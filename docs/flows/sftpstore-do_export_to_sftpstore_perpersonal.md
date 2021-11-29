# Create flow to export PerPersonal record to SFTPStore CSV file

## Requirements

* SFTPStore [authorization](../authorizations/sftp-store.md)
* SFTPStore [webhook](../webhooks/sftp-store-upload-file.md)
* SFTPStore [translator](../translators/parse_from_sftpstore_perpersonal_to_sftpstore_uplaod_request.md)
* SFTPStore [data-event](observers/SFTPStore-PerPersonal-throw_after_creating.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: do_export_to_sftpstore_perpersonal
    >- **Description**: Export the consolidated record of Cenit Personal identity to a CSV file.
    >- **Event**: SFTPStore | throw_after_creating
    >- **Translator**: SFTPStore | parse_from_sftpstore_perpersonal_to_sftpstore_uplaod_request
    >- **Source scope**: Event source
    >- **Webhook**: SFTPStore | upload_file
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

    > **Note**: For the name of the flow, the following format is recommended **do_\{*flow_type*\}\_to_\{*destination*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sftp-store-flow/snapshots-001.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sftp-store-flow/snapshots-203.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-204.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-205.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-206.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-207.png)
   
### Test flow (process)

   ![](../assets/snapshots/sftp-store-flow/snapshots-208.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-209.png)