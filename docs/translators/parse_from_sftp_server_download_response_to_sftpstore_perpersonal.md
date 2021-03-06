# Create parser-translator for download PerPersonal file from the SFTP-Server

## Requirements

* SFTPStore [source-data-type](data-types/SFTPStore-PerPersonal.md)
* Format and structure of the file to download from the SFTP-Server.
* Algorithm to [decrypt](algorithms/miesh-decrypt.md) data.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating translator of parser type

* Goto [translators](https://cenit.io/parser_transformation) module.
* Select the action [add new](https://cenit.io/parser_transformation/new) to create the new translator of parser type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: parse_from_sftp_server_response_to_sftpstore_perpersonal
    >- **Target data type**: [SFTPStore | PerPersonal](data-types/SFTPStore-PerPersonal.md)
    >- **Discard events**: false
    >- **Code**: the code snippet of template in Ruby language for processing the downloaded data.

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet for processing the downloaded encrypted file

```ruby
decryptData = begin
  ns_miesh = Cenit.namespace(:Miesh)
  decrypt = ns_miesh.algorithm(:decrypt)

  key = OpenSSL::Digest('SHA256').digest('mieah-passwd')
  iv = 'a2xhcgAAAAAAAAAA'

  decrypt.run([key, iv, data])
end

target_data = { filename:  parameters['filename'], content: decryptData }

record = target_data_type.create_from_json!(target_data, primary_field: [:filename])

# Preparing the parameters for the convert flow.
task.state[:target_id] = record.id
```

## Snapshots of the process

### Goto translator module

   ![](../assets/snapshots/common-trans/snapshots-002.png)
    
### Add new translator

   ![](../assets/snapshots/sftp-store-trans/snapshots-002.png)
