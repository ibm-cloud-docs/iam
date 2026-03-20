---

copyright:

  years: 2015, 2026
lastupdated: "2026-03-20"

keywords: service ID, service ID API key, lock service ID API key, delete service ID API key

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Managing service ID API keys
{: #serviceidapikeys}

Service IDs are created to enable access to your {{site.data.keyword.Bluemix}} services by applications hosted both inside and outside of {{site.data.keyword.cloud_notm}}. API keys are used by an application to authenticate as a particular service ID and are granted the access that is associated with that specific service ID.
{: shortdesc}

After you create a service ID, you can start creating API keys and assigning service policies. Each policy specifies the level of access that is allowed when the API key is used to authenticate with your services. For more information about creating a service ID and assigning policies, see [Creating and working with service IDs](/docs/account?topic=account-serviceids). For more information about the CLI commands that are used to manage service ID API keys, see [Managing IAM access, API keys, service IDs, and access groups](/docs/cli?topic=cli-ibmcloud_commands_iam).

Each API key that is associated with a service ID inherits the policy that is assigned to the service ID. For example, if you want one application to view resources within a service, you need to use an API key that is associated with a service ID that has a policy that is assigned with the Viewer role. If you want another application to be able to have full access within a service, then you need to use an API key that is associated with a second service ID that has a policy that is assigned with the Administrator role.

For some examples of how a service ID can be used, go to [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main) in the {{site.data.keyword.objectstorageshort}} documentation, or this {{site.data.keyword.sqlquery_notm}} video on [How to use the {{site.data.keyword.sqlquery_notm}} REST API](https://www.youtube.com/watch?v=jDZKF0CnUvU){: external}.
{: tip}

## Required access for managing service ID API keys
{: #required-access-serviceid-keys}

All users can create service IDs in an account, and they are the administrator for those IDs and can create the associated API key and access policies. However, account owners and users assigned the Administrator role on the IAM Identity service can manage the API keys for all service IDs in an account. Users can also be given access to a single service ID only, if the ID is specified when the administrator assigns the access.

If you are a user with the required access, you can view, update, and delete API keys for any service ID in the account. Go to the **API keys** page, and select the **All service ID API keys** option in the **View** menu to find an API key that you want to view details for, update, or delete.
{: ui}


## Creating an API key for a service ID
{: #create_service_key}
{: ui}

Create an API key to associate with a service ID in the console:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
2. If you don't have a service ID created, create the service ID.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Manage service ID**.
4. Click **API keys**.
5. Click **Create**.
6. Add a name and description to easily identify the API key.
7. Click **Create**.
8. Save your API key by copying or downloading it to secure location.

For security reasons, the API key is only available to be copied or downloaded at the time of creation. If the API key is lost, you must create a new API key.
{: note}


## Updating an API key for a service ID by using the console
{: #update_service_key}
{: ui}

You can update an API key by editing the name or description that is used to identify the key in the UI.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Manage service ID**.
3. Click **API keys**.
4. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit name & description**.

If you didn't create the service ID, but you are the account owner or an administrator for the IAM Identity service, you can update API keys for any service ID in the account. Go to the **API keys** page, and select the **All service ID API keys** option in the **View** menu to find the API key that you want to work with.
{: tip}

## Creating an API key for a service ID by using the CLI
{: #create_service_key_cli}
{: cli}

To create an API key for a service ID by using the CLI, you can use the [ibmcloud iam service-api-key-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_create) command.

```bash
ibmcloud iam service-api-key-create NAME (SERVICE_ID_NAME|SERVICE_ID_UUID) [-d, --description DESCRIPTION] [--file FILE] [-f, --force] [--lock]
```
{: codeblock}

## Updating an API key for a service ID by using the CLI
{: #update_service_key-cli}
{: cli}

To update an API key for a service ID by using the CLI, you can use the [ibmcloud iam service-api-key-update](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_update) command.

```bash
ibmcloud iam service-api-key-update NAME SERVICE_ID [-n, --name NEW_sNAME] [-d, --description DESCRIPTION] [-v, --version VERSION] [-f, --force]
```
{: codeblock}


## Locking a service ID's API key
{: #lockkey}
{: ui}

For API keys that represent the identity of the service ID, you can prevent the API key from being deleted by locking it. A locked API key is indicated by the **Locked** icon ![Locked icon](images/locked.svg "Locked") in the UI.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Service IDs**.
2. Identify the row of the service ID that you want to select an API key for, and select the name of the service ID.
3. Click **API keys**.
4. Hover on the row of the API key that you want to lock, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options.
5. Click **Lock API key**.

You can unlock your API key at any time to update, delete, or add an access policy, or to remove the API key.
{: tip}

## Locking or unlocking a service ID API key with the CLI
{: #lock_unlock_cli}
{: cli}

For API keys that represent the identity of the service ID, you can prevent the API key from being deleted by locking it. A locked API key is indicated by the **Locked** icon ![Locked icon](images/locked.svg "Locked") in the UI. To lock a service ID API key, use the following command:

```bash
ibmcloud iam service-api-key-lock (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [-f, --force]
```

Prerequisites
:   Endpoint, Login, Target

**Command Options**:

APIKEY_NAME (required)
:   Name of the API key, exclusive with APIKEY_UUID

APIKEY_UUID (required)
:   UUID of the API key, exclusive with APIKEY_NAME

SERVICE_ID_NAME (required)
:   Name of the service ID, exclusive with SERVICE_ID_UUID

SERVICE_ID_UUID (required)
:   UUID of the service ID, exclusive with SERVICE_ID_NAME

-f, --force
:   Lock without confirmation


**Examples**:

Lock service API key `sample-key` of service ID `sample-service`:

```bash
ibmcloud iam service-api-key-lock sample-key sample-service
```

To unlock a service ID API key, use the following command:

```bash
ibmcloud iam service-api-key-unlock (APIKEY_NAME|APIKEY_UUID) (SERVICE_ID_NAME|SERVICE_ID_UUID) [-f, --force]
```


## Deleting an API key for a service ID
{: #delete_service_key}
{: ui}

You can delete an API key that is associated with a service ID. However, deleting an API key that is used by an application removes the ability for that application to authenticate with your services.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
2. If you don't have a service ID created, create the service ID.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Manage service ID**.
4. Click **API keys**.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete**.

If you didn't create the service ID, but you are the account owner or an administrator for the IAM Identity service, you can delete API keys for any service ID in the account. Go to the **API keys** page, and select the **All service ID API keys** option in the **View** menu to find the API key that you want to work with.
{: tip}


## Deleting an API key for a service ID using the CLI
{: #delete_service_key-cli}
{: cli}

You can delete an API key that is associated with a service ID. However, deleting an API key that is used by an application removes the ability for that application to authenticate with your services. To delete an API key for a service ID by using the CLI, you can use the [ibmcloud iam service-api-key-delete](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_api_key_delete) command.

```bash
ibmcloud iam service-api-key-delete NAME SERVICE_ID [-f, --force]
```
{: codeblock}



## Creating an API key for a service ID using the API
{: #create_service_key-api}
{: api}

To create a service ID API key, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#create-api-key){: external} as shown in the following example.

```bash
curl -X POST 'https://iam.cloud.ibm.com/v1/apikeys' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -d '{
  "name": "Service-apikey",
  "description": "my service key",
  "iam_id": "IBMid-123WEREW",
  "account_id": "ACCOUNT_ID"
  "store_value": false
}'
```
{: codeblock}
{: curl}

```java
CreateApiKeyOptions createApiKeyOptions = new CreateApiKeyOptions.Builder()
    .name(apiKeyName)
    .iamId(iamId)
    .description("Example ApiKey")
    .build();

Response<ApiKey> response = service.createApiKey(createApiKeyOptions).execute();
ApiKey apiKey = response.getResult();
apikeyId = apiKey.getId();
System.out.println(apiKey.toString());
```
{: codeblock}
{: java}

```javascript
const params = {
  name: apikeyName,
  iamId: iamId,
  description: 'Example ApiKey',
};

iamIdentityService.createApiKey(params)
  .then(res => {
    apikeyId = res.result.id
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err);
  });
```
{: codeblock}
{: javascript}

```python
api_key = iam_identity_service.create_api_key(
  name=apikey_name,
  iam_id=iam_id
).get_result()

apikey_id = api_key['id']

print(json.dumps(api_key, indent=2))
```
{: codeblock}
{: python}

```go
createAPIKeyOptions := iamIdentityService.NewCreateAPIKeyOptions(apikeyName, iamID)
createAPIKeyOptions.SetDescription("Example ApiKey")

apiKey, response, err := iamIdentityService.CreateAPIKey(createAPIKeyOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(apiKey, "", "  ")
fmt.Println(string(b))
apikeyID = *apiKey.ID
```
{: codeblock}
{: go}

## Updating an API key for a service ID using the API
{: #update_service_key-api}
{: api}

To edit an API key for a service ID by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#update-api-key){: external} as shown in the following example:

```bash
curl -X PUT 'https://iam.cloud.ibm.com/v1/apikeys/APIKEY_UNIQUE_ID' -H 'Authorization: Bearer TOKEN' -H 'If-Match: <value of etag header from GET request>' -H 'Content-Type: application/json' -d '{
  "name": "Service-apikey",
  "description": "my service key"
}'
```
{: codeblock}
{: curl}

```java
UpdateApiKeyOptions updateApiKeyOptions = new UpdateApiKeyOptions.Builder()
    .id(apikeyId)
    .ifMatch(apikeyEtag)
    .description("This is an updated description")
    .build();

Response<ApiKey> response = service.updateApiKey(updateApiKeyOptions).execute();
ApiKey apiKey = response.getResult();
System.out.println(apiKey.toString());
```
{: codeblock}
{: java}

```javascript
const params = {
  id: apikeyId,
  ifMatch: apikeyEtag,
  description: 'This is an updated description',
};

iamIdentityService.updateApiKey(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err);
  });
```
{: codeblock}
{: javascript}

```python
api_key = iam_identity_service.update_api_key(
  id=apikey_id,
  if_match=apikey_etag,
  description='This is an updated description'
).get_result()

print(json.dumps(api_key, indent=2))
```
{: codeblock}
{: python}

```go
updateAPIKeyOptions := iamIdentityService.NewUpdateAPIKeyOptions(apikeyID, apikeyEtag)
updateAPIKeyOptions.SetDescription("This is an updated description")

apiKey, response, err := iamIdentityService.UpdateAPIKey(updateAPIKeyOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(apiKey, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}

## Locking and unlocking an API key for a service ID by using the API
{: #lock-unlock-serviceid-key-api}
{: api}

For API keys that represent the identity of the service ID, you can prevent the API key from being deleted by locking it.

### Locking an API key
{: #lock-service-key-api}
{: api}

To lock an API key for a service ID by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#lock-api-key){: external} as shown in the following example:

```bash
curl -X POST 'https://iam.cloud.ibm.com/v1/apikeys/APIKEY_UNIQUE_ID/lock' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
LockApiKeyOptions lockApiKeyOptions = new LockApiKeyOptions.Builder()
    .id(apikeyId)
    .build();

service.lockApiKey(lockApiKeyOptions).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  id: apikeyId,
};

iamIdentityService.lockApiKey(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err);
  });
```
{: codeblock}
{: javascript}

```python
response = iam_identity_service.lock_api_key(id=apikey_id)

print(response)
```
{: codeblock}
{: python}

```go
lockAPIKeyOptions := iamIdentityService.NewLockAPIKeyOptions(apikeyID)

response, err := iamIdentityService.LockAPIKey(lockAPIKeyOptions)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

### Unlocking an API key
{: #unlock-service-key-api}
{: api}

To unlock an API key for a service ID by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#unlock-api-key){: external} as shown in the following example:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/serviceids/SERVICE_ID_UNIQUE_ID/lock' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
UnlockServiceIdOptions unlockServiceIdOptions = new UnlockServiceIdOptions.Builder()
    .id(svcId)
    .build();

service.unlockServiceId(unlockServiceIdOptions).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  id: svcId,
};

iamIdentityService.unlockServiceId(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err);
    done(err);
  });
```
{: codeblock}
{: javascript}

```python
response = iam_identity_service.unlock_service_id(id=svc_id)

print(response)
```
{: codeblock}
{: python}

```go
unlockServiceIDOptions := iamIdentityService.NewUnlockServiceIDOptions(svcID)

response, err := iamIdentityService.UnlockServiceID(unlockServiceIDOptions)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

## Deleting an API key for a service ID using the API
{: #delete_service_key-api}
{: api}

To delete an API key by for a service ID using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api#delete-api-key){: external} as shown in the following example:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/apikeys/APIKEY_UNIQUE_ID' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
DeleteApiKeyOptions deleteApiKeyOptions = new DeleteApiKeyOptions.Builder()
    .id(apikeyId)
    .build();

service.deleteApiKey(deleteApiKeyOptions).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  id: apikeyId,
};

iamIdentityService.deleteApiKey(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err);
  });
```
{: codeblock}
{: javascript}

```python
delete_api_key(self,
        id: str,
        **kwargs
    ) -> DetailedResponse

response = iam_identity_service.delete_api_key(id=apikey_id)

print(response)
```
{: codeblock}
{: python}

```go
deleteAPIKeyOptions := iamIdentityService.NewDeleteAPIKeyOptions(apikeyID)

response, err := iamIdentityService.DeleteAPIKey(deleteAPIKeyOptions)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

## Before you begin
{: #create_service_key-terraform-prereq}
{: terraform}

Before you can manage service ID API keys by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

## Creating an API key for a service ID by using Terraform
{: #create_service_key-terraform}
{: terraform}

Use the following steps to create an API key for a service ID by using Terraform.

1. Create an argument in your `main.tf` file. The following example creates an API key for a service ID by using the `ibm_iam_service_api_key` resource, where `name` is a unique name to identify the service API key. You must need an IAM ID of the service in order to complete the task.

   ```terraform
   resource "ibm_iam_service_id" "serviceID" {
    name = "servicetest"
   }

   resource "ibm_iam_service_api_key" "testacc_apiKey" {
    name = "testapikey"
    iam_service_id = ibm_iam_service_id.serviceID.iam_id
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_api_key){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Updating an API key for a service ID by using Terraform
{: #update_service_key-terraform}
{: terraform}

Use the following steps to update an API key for a service ID by using Terraform:

1. Create an argument in your `main.tf` file. You can update the API key for a service ID by adding new values to the `name` and `iam_service_id` options in the following example.

   ```terraform
   resource "ibm_iam_service_id" "serviceID" {
    name = "servicetest"
   }

   resource "ibm_iam_service_api_key" "testacc_apiKey" {
    name = "testapikey"
    iam_service_id = ibm_iam_service_id.serviceID.iam_id
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_api_key){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Deleting an API key for a service ID by using Terraform
{: #delete_service_key-terraform}
{: terraform}

You must have created the API key for a service ID using the Terraform file. Use the following steps to delete an API key for a service ID by using Terraform.

1. The following example shows how to delete the API key for a service ID.

   ```terraform
   resource "ibm_iam_service_id" "serviceID" {
    name = "servicetest"
   }

   resource "ibm_iam_service_api_key" "testacc_apiKey" {
    name = "testapikey"
    iam_service_id = ibm_iam_service_id.serviceID.iam_id
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_service_api_key){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Reviewing leaked service ID API keys by using the console
{: #review-api-keys-serviceid-console}
{: ui}

If a leaked service ID API key is detected, you can use the console to review it. Complete the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} console.
1. Select the account that contains the leaked service ID API key.
1. Go to **Manage** > **Access** > **Service IDs**.
1. Select the name of the service ID.
1. Select **API keys**.
1. Select the name of the leaked API key to review it.

## Reviewing leaked service ID API keys by using the CLI
{: #review-api-keys-serviceid-cli}
{: cli}

If a leaked service ID API key is detected, you can use the CLI to review it. Complete the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.
1. Run the following command:

    ```bash
    ibmcloud iam service-api-key <API_key_ID> <service_id_name>
    ```
    {: codeblock}
