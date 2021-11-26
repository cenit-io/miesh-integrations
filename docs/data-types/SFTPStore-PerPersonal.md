# Create SFTPStore PerPersonal data-type

## Requirements

* The resource schema of new data-type.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating data-type

* Goto [data-types](https://cenit.io/json_data_type) module.
* Select the action [add new](https://cenit.io/json_data_type/new) to create the new data-type.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SFTPStore
    >- **Name**: PerPersonal
    >- **Schema**: { ...[JSON Schema](https://json-schema.org/)... }

    > **Note**: In schema you can define the main attrs and a rawData attr of type object to store all the information of the resource.

## Schema snippet

```JSON
{
  "type": "object",
  "properties": {
    "filename": {
      "type": "string"
    },
    "content": {
      "type": "string"
    }
  }
}
```

## Snapshots of the process

### Goto data-type module

   ![](../assets/snapshots/common-dt/snapshots-001.png)
   ![](../assets/snapshots/common-dt/snapshots-002.png)
   ![](../assets/snapshots/common-dt/snapshots-003.png)
    
### Add new data-type

   ![](../assets/snapshots/sftp-store-dt/snapshots-004.png)

