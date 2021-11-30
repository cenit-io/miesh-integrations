# Create a webhook to download a file from an SFTP-Server

## Requirements

* SFTPStore [connection](../connections/sftp-store.md)
* The resource-path, http-method and parameters to download file from the SFTP-Server.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating webhook

* Goto [webhooks](https://cenit.io/plain_webhook) module.
* Select the action [add new](https://cenit.io/plain_webhook/new) to create the new webhook.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: download_file
    >- **Path**: miesh/{{filename}}
    >- **Method**: get
    >- **Description**: Download file from SFTP-Server
    >- **Template Parameters**: filename

    > **Note**: For the name of the webhook, the following format is recommended **{*webhook_action*}\_{*webhook_noun*}**

## Snapshots of the process

### Goto webhook module

   ![](../assets/snapshots/sftp-store-wh/snapshots-001.png)
    
### Add new webhook

   ![](../assets/snapshots/sftp-store-wh/snapshots-002.png)
   ![](../assets/snapshots/sftp-store-wh/snapshots-003.png)
   ![](../assets/snapshots/sftp-store-wh/snapshots-004.png)
