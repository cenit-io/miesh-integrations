# Create a flow to convert PerPersonal records to a single consolidated record

## Requirements

* SAPSuccessFactors [translator](translators/parse_from_sapsf_to_sftpstore_perpersonal.md)
* Miesh [scheduler event](observers/Miesh-throw_once_a_day.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

<!-- tabs:start -->

#### **Scenario 01: Without associated event scheduler**

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: do_convert_from_sapsf_to_sftpstore_perpersonal
    >- **Description**: To convert all SAPSuccessFactors::PerPersonal records to a single record in SFTPStore with the content of a file in CSV format.
    >- **Translator**: [SAPSuccessFactors | parse_from_sapsf_to_sftpstore_perpersonal](translators/parse_from_sapsf_to_sftpstore_perpersonal.md)
    >- **Active**: true

#### **Scenario 02: With associated event scheduler**

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: do_convert_from_sapsf_to_sftpstore_perpersonal
    >- **Description**: To convert all SAPSuccessFactors::PerPersonal records to a single record in SFTPStore with the content of a file in CSV format.
    >- **Event**: [Miesh | throw_once_a_day](observers/Miesh-throw_once_a_day.md)
    >- **Translator**: [SAPSuccessFactors | parse_from_sapsf_to_sftpstore_perpersonal](translators/parse_from_sapsf_to_sftpstore_perpersonal.md)
    >- **Source scope**: All perpersonals
    >- **Active**: true

<!-- tabs:end -->

   > **Note**: For the convert flow name, the following format is recommended **do_convert_from_\{*origin*\}_to_\{*destination*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sap-sf-flow/snapshots-001.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sap-sf-flow/snapshots-203.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-208.png)
   
### Adding a scheduler event to the flow

   ![](../assets/snapshots/sap-sf-flow/snapshots-208.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-209.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-210.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-211.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-212.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-213.png)

### Test flow (process)

   ![](../assets/snapshots/sap-sf-flow/snapshots-204.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-205.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-206.png)
   ![](../assets/snapshots/sap-sf-flow/snapshots-207.png)
