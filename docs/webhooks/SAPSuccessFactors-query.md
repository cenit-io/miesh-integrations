# Create SAPSuccessFactors webhooks

## Requirements

* SAPSuccessFactors [connection](connections/SAPSuccessFactors-connection_sfapi.md)
* Review the SAPSuccessFactors Employee Central CompoundEmployee API specification.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* The resource-path, http-method and parameters of the API-Service.
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating webhook

* Goto [webhooks](https://cenit.io/plain_webhook) module.
* Select the action [add new](https://cenit.io/plain_webhook/new) to create the new webhook.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: query
    >- **Path**: soap
    >- **Method**: post
    >- **Headers**: Cookie = JSESSIONID={{jsessionid}}
    >- **Template Parameters**: limit = 200, jsessionid

    > **Note**: For the name of the webhook, the following format is recommended **{*webhook_action*}\_{*webhook_noun*}**

## Snapshots of the process

### Goto webhook module

   ![](../assets/snapshots/sap-sf-wh/snapshots-001.png)
    
### Add new webhook

   ![](../assets/snapshots/sap-sf-wh/snapshots-014.png)
   ![](../assets/snapshots/sap-sf-wh/snapshots-015.png)
   ![](../assets/snapshots/sap-sf-wh/snapshots-016.png)
   ![](../assets/snapshots/sap-sf-wh/snapshots-017.png)
