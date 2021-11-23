# Create SAP-SuccessFactors authorizations in CenitIO

## Requirements

* SAP-SuccessFactors user credentials. (_user-name, company-id and password_)
* Review the SAP-SuccessFactors API specification.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://help.sap.com/viewer/d599f15995d348a1b45ba5603e2aba9b/2111/en-US/5c8bca0af1654b05a83193b2922dcee2.html)
* Sign in at CenitIO.[<i class="fa fa-external-link" aria-hidden="true"></i>](https://cenit.io/users/sign_in)

## Creating Basic Authorization

* Goto [authorizations](https://cenit.io/authorization) module or direct to [basic-authorizations](https://cenit.io/basic_authorization) module.
* Select the action [add new](https://cenit.io/basic_authorization/new) to create the new authorization.
* Complete the fields of the form with the following information or those corresponding to your business:

    >- **Namespace**: SAPSuccessFactors
    >- **Name**: auth-basic
    >- **Username**: your-user-name@your-comapany-id
    >- **Password**: your-password
    
    > **Note**: For the name of the authorization, the following format is recommended **auth\-\{*type authorization*\}**

## Snapshots of the process

### Goto authorization module

   ![](../assets/snapshots/sap-sf-auth/snapshots-001.png)
   ![](../assets/snapshots/sap-sf-auth/snapshots-002.png)
    
### Add new authorization

   ![](../assets/snapshots/sap-sf-auth/snapshots-003.png)
   ![](../assets/snapshots/sap-sf-auth/snapshots-004.png)
   ![](../assets/snapshots/sap-sf-auth/snapshots-005.png)
   
### Authorize
   
   ![](../assets/snapshots/sap-sf-auth/snapshots-006.png)
   ![](../assets/snapshots/sap-sf-auth/snapshots-007.png)
   ![](../assets/snapshots/sap-sf-auth/snapshots-008.png)
