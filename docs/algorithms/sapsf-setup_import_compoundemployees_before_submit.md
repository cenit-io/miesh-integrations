# Create an algorithm to setup the import request before submitting it

## Requirements

* Identify the input data, the purpose and the output data.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit-io.github.io/docs/#/algorithms?id=algorithm39s-attributes)
* Identify the pagination strategy.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating the algorithm

* Goto [algorithms](https://cenit.io/algorithm) module.
* Select the action [add new](https://cenit.io/algorithm/new) to create the new algorithm.
* Complete the form fields with the information corresponding to the algorithm in question.

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: setup_import_compoundemployees_before_submit
    >- **Parameters**: options, task
    >- **Language**: Ruby
    >- **Code**: Code snippet written in the Ruby language.

    > **Note**: For the name of the algorithms before_submit, the following format is recommended **setup_{*flow_type*}_{*resource*}_before_submit** or **setup_{*flow_type*}_before_submit** when the same algorithm can be applied in several flows of the same type but over different resources.

## Code snippet

```ruby
get_jsessionid = Cenit.namespace(:SAPSuccessFactors).algorithm(:get_jsessionid)

options[:template_parameters]['jsessionid'] = get_jsessionid.run

options[:body] = begin
  builder = Nokogiri::XML::Builder.new_builder

  builder[:soapenv].Envelope('xmlns:soapenv' => 'http://schemas.xmlsoap.org/soap/envelope/', 'xmlns:urn' => 'urn:sfobject.sfapi.successfactors.com') {
    builder[:soapenv].Header
    builder[:soapenv].Body {
      builder[:urn].query {
        builder[:urn].queryString("SELECT person, personal_information FROM CompoundEmployee")
        builder[:urn].param {
          builder[:urn].name('batchSize')
          builder[:urn].value('200')
        }
      }
    }
  }

  builder.to_xml(encoding: 'UTF-8')
end
```

## Snapshots of the process

### Goto algorithm module

   ![](../assets/snapshots/common-algs/snapshots-001.png)
    
### Add new algorithm

   ![](../assets/snapshots/common-algs/snapshots-002.png)
   ![](../assets/snapshots/sap-sf-algs/snapshots-007.png)
