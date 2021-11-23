# Create SAP-SuccessFactors flows in CenitIO

## Requirements

* SAP-SuccessFactors [authorization](../authorizations/sap-success-factors.md)
* SAP-SuccessFactors [webhook](../webhooks/sap-success-factors.md)
* SAP-SuccessFactors [translator](../translators/sap-success-factors.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: do_import_perpersonal
    >- **Description**: Imports the records of the PerPersonal entity from SAP SuccessFactors and stores them transformed in cenit.
    >- **Translator**: SAPSuccessFactors | parse_from_sapsf_to_cenit_perpersonal
    >- **Webhook**: SAPSuccessFactors | get_personal_information
    >- **Authorization**: SAPSuccessFactors | auth-basic
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

    > **Note**: For the name of the flow, the following format is recommended **do_\{*action*\}\_\{*resource*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sap-sf-flow/snapshots-001.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sap-sf-flow/snapshots-003.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-004.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-005.png)
   
### Test flow (process)

   ![](../assets/snapshots/sap-sf-flow/snapshots-006.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-007.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-008.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-009.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-010.png)