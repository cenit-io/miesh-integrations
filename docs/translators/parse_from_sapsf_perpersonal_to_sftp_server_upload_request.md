# Create template-translator for upload the PerPersonal records to SFTP-Server file

## Requirements

* SAPSuccessFactors [source-data-type](../data-types/SAPSuccessFactors-PerPersonal.md)
* Format and structure of the file to upload to the SFTP-Server.
* Algorithm to encrypt data.[<i class="fa fa-external-link" aria-hidden="true"></i>](../algorithms/miesh-encrypt.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating translator of template type

* Goto [translators](https://cenit.io/template) module.
* Select the action [add new](https://cenit.io/template/new) to create the new translator of template type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: parse_from_sapsf_perpersonal_to_sftp_server_upload_request
    >- **Source data type**: SAPSuccessFactors | PerPersonal
    >- **MIME type**: text/csv
    >- **File extension**: csv
    >- **Bulk source**: true
    >- **Code**: the code snippet of template in Ruby language to prepare raw o encrypt file.

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}**

## Code snippet to prepare the file for upload

<!-- tabs:start -->

#### **Raw file**

```ruby
body = ''

sources.each do |item| 
  body << item.personIdExternal << ','
  body << item.firstName << ',' 
  body << item.lastName << "\n"
end  

template_parameters['filename'] = "perpersonal-#{DateTime.now.iso8601}.csv"

body
```

#### **Encrypted file**

```ruby
body = ''

sources.each do |item| 
  body << item.personIdExternal << ','
  body << item.firstName << ',' 
  body << item.lastName << "\n"
end  

template_parameters['filename'] = "perpersonal-#{DateTime.now.iso8601}-encrypt.csv"

encrypt = Cenit.namespace(:Miesh).algorithm(:encrypt)
key = OpenSSL::Digest('SHA256').digest('mieah-passwd')
iv = 'a2xhcgAAAAAAAAAA'

encrypt.run([key, iv, body])
```

<!-- tabs:end -->

## Snapshots of the process

### Goto translator module

   ![](assets/snapshots/sap-sf-trans/snapshots-001.png)
    
### Add new translator

   ![](assets/snapshots/sap-sf-trans/snapshots-003.png)
   
