# Create SAP-SuccessFactors translators in CenitIO

## Requirements

* SAP-SuccessFactors [data-type](../data-types/sap-success-factors.md)
* Review the SAP-SuccessFactors API specification.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* The resource schema in the API-Service response.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating parser translator

* Goto [translators](https://cenit.io/parser_transformation) module.
* Select the action [add new](https://cenit.io/parser_transformation/new) to create the new translator.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: parse_from_sapsf_to_cenit_perpersonal
    >- **Target data type**: SAPSuccessFactors | PerPersonal

    > **Note**: For the name of the translator, the following format is recommended **parse_from\_\{*origin*\}\_to\_\{*destination*\}\_\{*resource*\}**

## Snapshots of the process

### Goto translator module

   ![](../assets/snapshots/sap-sf-trans/snapshots-001.png)
    
### Add new translator

   ![](../assets/snapshots/sap-sf-trans/snapshots-002.png)
   
