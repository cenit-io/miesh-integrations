# Create flow to import PerPersonal from SFTP-Server

## Requirements

* SFTPStore [authorization](authorizations/SFTPStore-auth_basic.md)
* SFTPStore [webhook](webhooks/SFTPStore-download_file.md)
* SFTPStore [translator](translators/parse_from_sftp_server_download_response_to_sftpstore_perpersonal.md)
* SFTPStore [before-submit](algorithms/sftpstore-setup_import_before_submit.md)
* SFTPStore [after-callback](algorithms/sftpstore-convert_import_perpersonal_after_callback.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

<!-- tabs:start -->

#### **Scenario 01: Simple**

    >- **Namespace**: SFTPStore
    >- **Name**: do_import_from_sftp_server_perpersonal
    >- **Description**: Import the file with PerPersonal data from SFTP server
    >- **Translator**: [SFTPStore | parse_from_sftp_server_response_to_sftpstore_perpersonal](translators/parse_from_sftp_server_download_response_to_sftpstore_perpersonal.md)
    >- **Webhook**: [SFTPStore | download_file](webhooks/SFTPStore-download_file.md)
    >- **Authorization**: [SFTPStore | auth-basic](authorizations/SFTPStore-auth_basic.md)
    >- **Before submit**: 
    >   - [SFTPStore | setup_import_before_submit](algorithms/sftpstore-setup_import_before_submit)
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

#### **Scenario 02: Connected with convert flows**

    >- **Namespace**: SFTPStore
    >- **Name**: do_import_from_sftp_server_perpersonal
    >- **Description**: Import the file with PerPersonal data from SFTP server
    >- **Translator**: [SFTPStore | parse_from_sftp_server_response_to_sftpstore_perpersonal](translators/parse_from_sftp_server_download_response_to_sftpstore_perpersonal.md)
    >- **Webhook**: [SFTPStore | download_file](webhooks/SFTPStore-download_file.md)
    >- **Authorization**: [SFTPStore | auth-basic](authorizations/SFTPStore-auth_basic.md)
    >- **Before submit**: 
    >   - [SFTPStore | setup_import_before_submit](algorithms/sftpstore-setup_import_before_submit)
    >- **After process callbacks**: 
    >   - [SFTPStore | convert_import_perpersonal_after_callback](algorithms/sftpstore-convert_import_perpersonal_after_callback.md)
    >- **Active**: true
    >- **Notify request**: true
    >- **Notify response**: true

<!-- tabs:end -->

   > **Note**: For the name of the import flow, the following format is recommended **do_import_from\_\{*origin*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sftp-store-flow/snapshots-001.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sftp-store-flow/snapshots-303.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-303b.png)

### Test flow (process)

   ![](../assets/snapshots/sftp-store-flow/snapshots-304.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-305.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-306.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-307.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-308.png)
