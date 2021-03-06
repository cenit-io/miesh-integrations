# Create parser-translator for PerPersonal api response

## Requirements

* SAPSuccessFactors [source-data-type](data-types/SAPSuccessFactors-PerPersonal.md)
* Review the SAPSuccessFactors API specification.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* The resource schema in the API-Service response.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating translator of parser type

* Goto [translators](https://cenit.io/parser_transformation) module.
* Select the action [add new](https://cenit.io/parser_transformation/new) to create the new translator of parser type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: parse_from_sapsf_api_response_to_sapsf_perpersonal
    >- **Target data type**: [SAPSuccessFactors | PerPersonal](data-types/SAPSuccessFactors-PerPersonal.md)
    >- **Code**: the code snippet of parser in Ruby language

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet

```ruby
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
```

## Snapshots of the process

### Goto translator module

   ![](../assets/snapshots/common-trans/snapshots-002.png)
    
### Add new translator

   ![](../assets/snapshots/sap-sf-trans/snapshots-002.png)
   
