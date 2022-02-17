# Miesh Integrations

<!-- tabs:start -->

## **Scenario 01**
## Scenario 01

Simple PerPersonal import and export processes with a single data type.

In this scenario, the records are imported into a data-type and then when the export process is executed, it reads the 
records of the same data-type, prepares and sends the file to the cloud.

### Import PerPersonal from SAP-SF

1. Create the basic-authorization 
2. Create the connection for OData-API
3. Create the webhook for get perpersonal information
4. Create the data-type PerPersonal
5. Create the parser translator
6. Create the before-submit algorithm to setup request
7. Create the import-flow


## Code

```javascript
const dotenv = require('dotenv')
const axios = require('axios');

dotenv.config();

axios.defaults.baseURL = process.env['BASE_URL'] || 'https://cenit.io/api/v2/';
axios.defaults.headers.common['Content-Type'] = 'application/json'
axios.defaults.headers.common['X-Tenant-Access-Key'] = process.env['X_TENANT_ACCESS_KEY']
axios.defaults.headers.common['X-Tenant-Access-Token'] = process.env['X_TENANT_ACCESS_TOKEN']

function request(options) {
  const axiosInstance = axios.create();

  return axiosInstance(options).then(
    (response) => {
      if (response.data.errors) throw { response: response }
      return response.data
    }
  ).catch(
    (err) => {
      throw (err.response ? err.response.data : err.message)
    }
  );
}

const namespace = 'APITest_SAPSF'

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_basic_authorization
 */
async function create_authorization() {
  const item = await request({
    method: 'POST',
    url: 'setup/basic_authorization',
    data: {
      namespace: namespace,
      name: 'auth_basic',
      username: process.env['SAPSF_USERNAME'],
      password: process.env['SAPSF_PASSWORD'],
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_connection
 */
async function create_connection() {
  const item = await request({
    method: 'POST',
    url: 'setup/connection',
    data: {
      namespace: namespace,
      name: 'connection_odata',
      url: 'https://api2.successfactors.eu/odata/v2/',
      authorization: { _reference: true, namespace: namespace, name: 'auth_basic' },
      parameters: [
        { key: '$format', value: 'JSON' }
      ]
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_plain_webhook
 */
async function create_plain_webhook() {
  const item = await request({
    method: 'POST',
    url: 'setup/plain_webhook',
    data: {
      namespace: namespace,
      name: 'get_personal_information',
      path: 'PerPersonal',
      method: 'get',
      description: 'Query Personal Information',
      parameters: [
        { key: 'customPageSize', value: '{{limit}}' },
        { key: '$skiptoken', value: '{{skiptoken}}' },
      ],
      template_parameters: [
        { key: 'limit', value: '200' },
        { key: 'skiptoken' },
      ]
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_json_data_type
 */
async function create_json_data_type() {
  const item = await request({
    method: 'POST',
    url: 'setup/json_data_type',
    data: {
      namespace: namespace,
      name: 'PerPersonal',
      code: JSON.stringify({
        type: 'object',
        properties: {
          personIdExternal: {
            type: 'string'
          },
          firstName: {
            type: 'string'
          },
          lastName: {
            type: 'string'
          },
          rawData: {
            type: 'object',
            visible: false
          }
        }
      })
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_ruby_parser
 */
async function create_ruby_parser() {
  const code = `
    data = begin 
      JSON.parse(data, symbolize_names: true)
    rescue
      Cenit.fail(data)
    end
    
    items = data[:d][:results]
    
    items.each do |item|
      target = {
        personIdExternal: item[:personIdExternal],
        firstName: item[:firstName],
        lastName: item[:lastName],
        rawData: item
      }
    
      target_data_type.create_from_json!(target, primary_field: [:personIdExternal])
    end
    
    # Preparing the request of the next page.
    begin
      task.state[:next_page_info] ||= {}
      query_params = URI.try(:decode_www_form, data[:d][:__next] || '').to_h
      if query_params['$skiptoken']
        task.state[:next_page_info] = {
          skiptoken: query_params['$skiptoken'],
          current_page: task.state[:next_page_info][:current_page].to_i + 1,
        }
      else
        task.state[:next_page_info] = nil
      end
    end
  `;

  const item = await request({
    method: 'POST',
    url: 'setup/ruby_parser',
    data: {
      namespace: namespace,
      name: 'parse_from_sapsf_api_response_to_sapsf_perpersonal',
      target_data_type: { _reference: true, namespace: namespace, name: 'PerPersonal' },
      code: code,
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_algorithm
 */
async function create_before_submit_algorithm() {
  const code = `
    # Set the number of items per page.
    options[:template_parameters]['limit'] = 200
    
    # Set the token of the next page to import.
    options[:template_parameters]['skiptoken'] = task.state[:next_page_info][:skiptoken] unless task.state[:next_page_info].blank?
  `;

  const item = await request({
    method: 'POST',
    url: 'setup/algorithm',
    data: {
      namespace: namespace,
      name: 'before_submit_for_import',
      language: 'ruby',
      code: code,
      parameters: [
        { name: 'options', required: true },
        { name: 'task', required: true },
      ],
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_algorithm
 */
async function create_after_callback_algorithm() {
  const code = `
    # Limit the number of pages to import for testing.
    task.state[:next_page_info] = nil if task.state[:next_page_info][:current_page] == 3
    
    task.run_again unless task.state[:next_page_info].blank?
  `;

  const item = await request({
    method: 'POST',
    url: 'setup/algorithm',
    data: {
      namespace: namespace,
      name: 'after_callback_for_import',
      language: 'ruby',
      code: code,
      parameters: [
        { name: 'task', required: true },
      ],
    }
  });

  return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_flow
 */
async function create_flow_import() {
  const item = await request({
    method: 'POST',
    url: 'setup/flow',
    data: {
      namespace: namespace,
      name: 'do_import_from_sapsf_perpersonal',
      description: 'Imports the records of the PerPersonal entity from SAP SuccessFactors and stores them transformed in cenit.',
      notify_request: true,
      notify_response: true,
      active: true,
      translator: {
        _reference: true, namespace: namespace, name: 'parse_from_sapsf_api_response_to_sapsf_perpersonal'
      },
      webhook: {
        _reference: true, namespace: namespace, name: 'get_personal_information'
      },
      before_submit: {
        _reference: true, namespace: namespace, name: 'before_submit_for_import'
      },
      after_process_callbacks: [
        { _reference: true, namespace: namespace, name: 'after_callback_for_import' }
      ],
    }
  });

  return item;
};

async function create_scenario_01_import() {
  try {
    console.log('STEP-01: Create the authorization');
    await create_authorization();

    console.log('STEP-02: Create the connection');
    await create_connection();

    console.log('STEP-03: Create the plain_webhook');
    await create_plain_webhook();

    console.log('STEP-04: Create the json_data_type');
    await create_json_data_type();

    console.log('STEP-05: Create the ruby_parser');
    await create_ruby_parser();

    console.log('STEP-06: Create the before_submit algorithm to set pagination options');
    await create_before_submit_algorithm();

    console.log('STEP-07: Create the after_callback algorithm to start processing the next page');
    await create_after_callback_algorithm();

    console.log('STEP-08: Create the flow to import the records');
    await create_flow_import();

  } catch (err) {
    console.log(JSON.stringify(err, null, 2))
  }
};

create_scenario_01_import();
```


### Export PerPersonal records to SFTP-Server

1. Create the basic-authorization for the SFTP-Server
2. Create the connection for the SFTP-Server
3. Create the webhook for upload a file
4. Create the encryption algorithm
5. Create the template translator
6. Create the export-flow
7. Create a after-callback algorithm to process export 
8. Update the import-flow to add the new after-callback algorithm

## Code

```javascript
const dotenv = require('dotenv')
const axios = require('axios');

dotenv.config();

axios.defaults.baseURL = process.env['BASE_URL'] || 'https://cenit.io/api/v2/';
axios.defaults.headers.common['Content-Type'] = 'application/json'
axios.defaults.headers.common['X-Tenant-Access-Key'] = process.env['X_TENANT_ACCESS_KEY']
axios.defaults.headers.common['X-Tenant-Access-Token'] = process.env['X_TENANT_ACCESS_TOKEN']

function request(options) {
    const axiosInstance = axios.create();

    return axiosInstance(options).then(
        (response) => {
            if (response.data.errors) throw { response: response }
            return response.data
        }
    ).catch(
        (err) => {
            throw (err.response ? err.response.data : err.message)
        }
    );
}

const namespace_source = 'APITest_SAPSF'
const namespace_target = 'APITest_SFTPStore'
const namespace_common = 'APITest_Utils'

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_basic_authorization
 */
async function create_authorization() {
    const item = await request({
        method: 'POST',
        url: 'setup/basic_authorization',
        data: {
            namespace: namespace_target,
            name: 'auth_basic',
            username: process.env['SFTPStore_USERNAME'],
            password: process.env['SFTPStore_PASSWORD'],
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_connection
 */
async function create_connection() {
    const item = await request({
        method: 'POST',
        url: 'setup/connection',
        data: {
            namespace: namespace_target,
            name: 'connection_sftp',
            url: process.env['SFTPStore_CONNECTION_URL'],
            authorization: { _reference: true, namespace: namespace_target, name: 'auth_basic' }
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_plain_webhook
 */
async function create_plain_webhook() {
    const item = await request({
        method: 'POST',
        url: 'setup/plain_webhook',
        data: {
            namespace: namespace_target,
            name: 'upload_file',
            path: ' miesh/{{filename}}',
            method: 'put',
            description: 'Upload file to SFTP-Server',
            template_parameters: [
                { key: 'filename' },
            ]
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_algorithm
 */
async function create_encrypt_algorithm() {
    const code = `
    cipher = OpenSSL::Cipher.try(:new, 'AES-256-CBC')
    cipher.encrypt # set cipher to be encryption mode
    cipher.key = key
    cipher.iv = iv
    
    encrypted = ''
    encrypted << cipher.update(data)
    encrypted << cipher.final
    
    Base64.encode64(encrypted).gsub(/\\n/, '')
  `;

    const item = await request({
        method: 'POST',
        url: 'setup/algorithm',
        data: {
            namespace: namespace_common,
            name: 'encrypt',
            language: 'ruby',
            code: code,
            parameters: [
                { name: 'key', required: true },
                { name: 'iv', required: true },
                { name: 'data', required: true },
            ],
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_ruby_template
 */
async function create_ruby_template() {
    const code = `
    body = ''
    sources.each do |item| 
      body << item.personIdExternal << ','
      body << item.firstName << ',' 
      body << item.lastName << "\\n"
    end  
    template_parameters['filename'] = "perpersonal-#{DateTime.now.iso8601}-encrypt.csv"
    
    encrypt = Cenit.namespace(:${namespace_common}).algorithm(:encrypt)
    key = OpenSSL::Digest('SHA256').digest('mieah-passwd')
    iv = 'a2xhcgAAAAAAAAAA'
    
    encrypt.run([key, iv, body])
  `;

    const item = await request({
        method: 'POST',
        url: 'setup/ruby_template',
        data: {
            namespace: namespace_source,
            name: 'parse_from_sapsf_perpersonal_to_sftp_server_upload_request',
            mime_type: "text/csv",
            file_extension: "csv",
            bulk_source: true,
            source_data_type: { _reference: true, namespace: namespace_source, name: 'PerPersonal' },
            code: code,
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_flow
 */
async function create_flow_export() {
    const item = await request({
        method: 'POST',
        url: 'setup/flow',
        data: {
            namespace: namespace_source,
            name: 'do_export_to_sftp_server_perpersonal',
            description: 'Export the records of the PerPersonal entity from the APITest_SAPSF to an SFTP Server.',
            notify_request: true,
            notify_response: true,
            active: true,
            translator: {
                _reference: true,
                namespace: namespace_source,
                name: 'parse_from_sapsf_perpersonal_to_sftp_server_upload_request'
            },
            webhook: {
                _reference: true, namespace: namespace_target, name: 'upload_file'
            },
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/create_algorithm
 */
async function create_after_callback_algorithm() {
    const code = `
        ns_sapsf = Cenit.namespace(:${namespace_source})
        flow = ns_sapsf.flow(:do_export_to_sftp_server_perpersonal)
        flow.process if task.state[:next_page_info].blank?
  `;

    const item = await request({
        method: 'POST',
        url: 'setup/algorithm',
        data: {
            namespace: namespace_source,
            name: 'after_callback_for_start_export',
            language: 'ruby',
            code: code,
            parameters: [
                { name: 'task', required: true },
            ],
        }
    });

    return item;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/get_flows
 */
async function get_flow_import_id() {
    const response = await request({
        method: 'GET',
        url: 'setup/flow',
        headers: {
            'X-Query-Selector': JSON.stringify({
                namespace: namespace_source,
                name: 'do_import_from_sapsf_perpersonal'
            })
        },
        params: { limit: 1, only: 'id' }
    });

    return response.flows[0].id;
};

/**
 * @see https://cenit-io.github.io/api-v2-specs/#operation/update_flow
 */
async function update_flow_import() {
    const item_id = await get_flow_import_id();

    const item = await request({
        method: 'POST',
        url: `setup/flow/${item_id}`,
        data: {
            after_process_callbacks: [
                { _reference: true, namespace: namespace_source, name: 'after_callback_for_import' },
                { _reference: true, namespace: namespace_source, name: 'after_callback_for_start_export' }
            ],
        }
    });

    return item;
};

async function create_scenario_01_export() {
    try {
        console.log('STEP-01: Create the authorization');
        await create_authorization();

        console.log('STEP-02: Create the connection');
        await create_connection();

        console.log('STEP-03: Create the plain_webhook');
        await create_plain_webhook();

        console.log('STEP-04: Create the encryption algorithm');
        await create_encrypt_algorithm();

        console.log('STEP-05: Create the ruby_template');
        await create_ruby_template();

        console.log('STEP-06: Create the flow to export');
        await create_flow_export();

        console.log('STEP-07: Create the after_callback algorithm for start export');
        await create_after_callback_algorithm();

        console.log('STEP-08: Update the import flow for add the new after_callback');
        await update_flow_import();

    } catch (err) {
        console.log(JSON.stringify(err, null, 2))
    }
};

create_scenario_01_export();
```

<!-- tabs:end -->

<hr />

> For more details see also [CenitIO API Specifications (v2)](https://cenit-io.github.io/api-v2-specs/)