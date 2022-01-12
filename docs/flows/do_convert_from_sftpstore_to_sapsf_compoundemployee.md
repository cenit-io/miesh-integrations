# Create a flow to convert PerPersonal consolidated record to CompoundEmployee separate records

## Requirements

* SFTPStore [translator](translators/parse_from_sftpstore_to_sapsf_compoundemployee.md)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating flow

* Goto [flows](https://cenit.io/flow) module.
* Select the action [add new](https://cenit.io/flow/new) to create the new flow.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: do_convert_from_sftpstore_to_sapsf_compoundemployee
    >- **Description**: To extract the imported data and store it in separate records in SAPSuccessFactors:CompoundEmployee data-type.
    >- **Translator**: [SFTPStore | parse_from_sftpstore_to_sapsf_compoundemployee](translators/parse_from_sftpstore_to_sapsf_compoundemployee.md)
    >- **Active**: true

    > **Note**: For the convert flow name, the following format is recommended **do_convert_from_\{*origin*\}_to_\{*destination*\}**

## Snapshots of the process

### Goto flow module

   ![](../assets/snapshots/sftp-store-flow/snapshots-001.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-002.png)
    
### Add new flow

   ![](../assets/snapshots/sftp-store-flow/snapshots-503.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-504.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-505.png)
   
### Test flow (process)

   ![](../assets/snapshots/sftp-store-flow/snapshots-506.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-507.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-508.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-509.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-510.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-511.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-512.png)
   ![](../assets/snapshots/sftp-store-flow/snapshots-513.png)
