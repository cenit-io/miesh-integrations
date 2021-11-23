# Create SFTP-Store webhooks in CenitIO

## Requirements

* SFTP-Store [connection](../connections/sftp-store.md)
* The resource-path, http-method and parameters of the SFTP-Store.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating webhook

* Goto [webhooks](https://cenit.io/plain_webhook) module.
* Select the action [add new](https://cenit.io/plain_webhook/new) to create the new webhook.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: upload_file
    >- **Path**: miesh/{{filename}}
    >- **Method**: put
    >- **Description**: Upload file to SFTP-Store
    >- **Template Parameters**: filename

## Snapshots of the process

### Goto webhook module

   ![](../assets/snapshots/sftp-store-wh/snapshots-001.png)
    
### Add new webhook

   ![](../assets/snapshots/sftp-store-wh/snapshots-002.png)
   ![](../assets/snapshots/sftp-store-wh/snapshots-003.png)
   ![](../assets/snapshots/sftp-store-wh/snapshots-004.png)