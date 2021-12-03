# Create a flow to convert PerPersonal records to a single consolidated record

## Requirements

* SAPSuccessFactors [translator](../translators/parse_from_sapsf_to_sftpstore_perpersonal.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: do_convert_from_sapsf_to_sftpstote_perpersonal
    >- **Description**: To convert all SAPSuccessFactors::PerPersonal records to a single record in SFTPStore with the content of a file in CSV format.
    >- **Translator**: SAPSuccessFactors | parse_from_sapsf_to_sftpstore_perpersonal
    >- **Active**: true

    > **Note**: For the convert flow name, the following format is recommended **do_convert_from_\{*origin*\}_to\_{*destination*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sftp-store-flow/snapshots-001.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sftp-store-flow/snapshots-103.png)
   
### Test flow (process)

   ![](../assets/snapshots/sftp-store-flow/snapshots-104.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-105.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-106.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-107.png)
