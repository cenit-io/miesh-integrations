# Create flow to export PerPersonal records to SFTP Server CSV file

## Requirements

* SFTPStore [authorization](../authorizations/SFTPStore-auth_basic.md)
* SFTPStore [webhook](../webhooks/SFTPStore-upload_file.md)
* SAPSuccessFactors [translator](translators/parse_from_sapsf_perpersonal_to_sftp_server_upload_request.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: do_export_to_sftp_server_perpersonal
    >- **Description**: Export the records of the PerPersonal entity from the SAPSuccessFactors to an SFTP Server.
    >- **Translator**: [SAPSuccessFactors | parse_from_sapsf_perpersonal_to_sftp_server_upload_request](translators/parse_from_sapsf_perpersonal_to_sftp_server_upload_request.md)
    >- **Webhook**: [SFTPStore | upload_file](../webhooks/SFTPStore-upload_file.md)
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

    > **Note**: For the name of the export flow, the following format is recommended **do_export_to_\{*destination*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sftp-store-flow/snapshots-001.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sftp-store-flow/snapshots-003.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-004.png)
   
### Test flow (process)

   ![](../assets/snapshots/sftp-store-flow/snapshots-005.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-006.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-007.png)
