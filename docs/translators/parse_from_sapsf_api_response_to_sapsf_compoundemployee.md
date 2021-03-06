# Create parser-translator for CompoundEmployee api response

## Requirements

* SAPSuccessFactors [source-data-type](data-types/SAPSuccessFactors-CompoundEmployee.md)
* Review the SAPSuccessFactors Employee Central CompoundEmployee API specification.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* Review Ruby Nokogiri::XML documentation.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://www.rubydoc.info/github/sparklemotion/nokogiri/Nokogiri/XML)
* The resource schema in the API-Service response.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating translator of parser type

* Goto [translators](https://cenit.io/parser_transformation) module.
* Select the action [add new](https://cenit.io/parser_transformation/new) to create the new translator of parser type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: parse_from_sapsf_api_response_to_sapsf_compoundemployee
    >- **Target data type**: [SAPSuccessFactors | CompoundEmployee](data-types/SAPSuccessFactors-CompoundEmployee.md)
    >- **Code**: the code snippet of parser in Ruby language

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet
```ruby
xml = Nokogiri::XML(data) { |config| config.strict.noblanks }
result = xml.at_xpath('//ns1:result', 'ns1' => 'urn:sfobject.sfapi.successfactors.com')

data = Hash.from_xml(result.to_xml).deep_symbolize_keys

items = data[:result][:sfobject]

items.each do |item|
  item[:person][:personal_information] = item[:person][:personal_information].first if item[:person][:personal_information].is_a?(Array)

  target = {
    personIdExternal: item[:person][:person_id_external],
    firstName: item[:person][:personal_information][:first_name],
    lastName: item[:person][:personal_information][:last_name],
    rawData: item
  }

  target_data_type.create_from_json!(target, primary_field: [:personIdExternal])
end

# Preparing the request of the next page.
begin
  task.state[:next_page_info] ||= {}
  if data[:result][:hasMore] == 'true'
    task.state[:next_page_info] = {
      query_session_id: data[:result][:querySessionId],
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

   ![](../assets/snapshots/sap-sf-trans/snapshots-004.png)
   
