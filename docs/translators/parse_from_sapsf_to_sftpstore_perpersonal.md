# Create convert-translator for PerPersonal

## Requirements

* SAPSuccessFactors [source-data-type](../data-types/SAPSuccessFactors-PerPersonal.md)
* SFTPStore [target-data-type](../data-types/SAPSuccessFactors-PerPersonal.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating convert-translator

* Goto [translators](https://cenit.io/ruby_converter) module.
* Select the action [add new](https://cenit.io/ruby_converter/new) to create the new translator of convert type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: parse_from_sapsf_to_sftpstore_perpersonal
    >- **Source data type**: SAPSuccessFactors | PerPersonal
    >- **Target data type**: SFTPStore | PerPersonal
    >- **Code**: the code snippet of converter in Ruby language

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet

```ruby
content = '';

sources.each do |item|
  # Add and customize the row of csv file  
  content << item.personIdExternal << ','
  content << item.firstName << ',' 
  content << item.lastName << "\n"
end

date = DateTime.now.iso8601
target_data = { filename:  "perpersonal-#{date}.csv", content: content }

target_data_type.create_from_json!(target_data, primary_field: [:filename])
```

## Snapshots of the process

### Goto translator module

   ![](../assets/snapshots/sftp-store-trans/snapshots-001.png)
    
### Add new translator

   ![](../assets/snapshots/sftp-store-trans/snapshots-002.png)
   
