# Create SFTP-Store flow to export PerPersonal to CSV file

## Requirements

* SFTP-Store [authorization](../authorizations/sftp-store.md)
* SFTP-Store [webhook](../webhooks/sftp-store-upload-file.md)
* SFTP-Store [translator](../translators/parse_from_sapsf_perpersonal_to_sftpstore_uplaod_request.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: do_export_perpersonal
    >- **Description**: Export the records of the PerPersonal entity from Cenit to CSV file.
    >- **Translator**: SFTPStore | parse_from_cenit_perpersonal_to_sftp_csv
    >- **Webhook**: SFTPStore | upload_file
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

    > **Note**: For the name of the flow, the following format is recommended **do_\{*flow_type*\}\_\{*resource*\}**

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
