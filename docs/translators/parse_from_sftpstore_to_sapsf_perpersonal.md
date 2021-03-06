# Create convert-translator for PerPersonal

## Requirements

* SFTPStore [source-data-type](data-types/SFTPStore-PerPersonal.md)
* SAPSuccessFactors [target-data-type](data-types/SAPSuccessFactors-PerPersonal.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating translator of converter type

* Goto [translators](https://cenit.io/ruby_converter) module.
* Select the action [add new](https://cenit.io/ruby_converter/new) to create the new translator of convert type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: parse_from_sftpstore_to_sapsf_perpersonal
    >- **Source data type**: [SFTPStore | PerPersonal](data-types/SFTPStore-PerPersonal.md)
    >- **Target data type**: [SAPSuccessFactors | PerPersonal](data-types/SAPSuccessFactors-PerPersonal.md)
    >- **Source handler**: true
    >- **Code**: the code snippet of converter in Ruby language

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet

```ruby
sources.each do |record| 
  record.content.strip.split(/[\n\r]+/).map do |line|
    personIdExternal, firstName, lastName = line.split(',')
    target_data = { personIdExternal: personIdExternal, firstName: firstName, lastName: lastName }
    target_data_type.create_from_json!(target_data, primary_field: [:personIdExternal])
  end
end
```

## Snapshots of the process

### Goto translator module

   ![](../assets/snapshots/common-trans/snapshots-001.png)
    
### Add new translator

   ![](../assets/snapshots/sftp-store-trans/snapshots-001.png)
   