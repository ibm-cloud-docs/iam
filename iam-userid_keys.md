---

copyright:

  years: 2015, 2026
lastupdated: "2026-03-20"

keywords: API key, user API keys, IBM Cloud API keys, manage user keys, create API key

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Managing user API keys
{: #userapikey}

A federated user or nonfederated user can create an API key to use in the CLI or as part of automation to log in as your user identity. You can use the console, CLI, or API to manage your {{site.data.keyword.cloud}} API keys by listing your keys, creating keys, update keys, or delete keys.
{: shortdesc}

The API key inherits all assigned access for the user identity for which it is created, and the access is not limited to just the account where the API key is created because it inherits any policies that are assigned to the user. So, if the user has access to resources from multiple accounts, then the API key inherits the access from all accounts. Therefore, it is possible that a user's API key can be used to generate a token and access resources that a user has access to outside of the account where the API key was created.







The API key that is associated with your user identity has all of the access you're entitled to across any account that you are a member of. For this reason, you must be cautious with how you use your API key. For example, an {{site.data.keyword.cloud_notm}} service might need to act on behalf of a user or access services that are not IAM-enabled, so the service might request a user API key. In these cases, create an API key that's associated with a functional ID that is assigned the minimum level of access that is required to work with the service.

A functional ID is a user ID created to represent a program, application, or service. The functional ID can be invited to an account and assigned only the access for a particular purpose, such as interacting with a specific resource or application. The functional ID should be granted only the minimum level access in a single account that is needed for the specific function for which it was created.

If you are applying a trusted profile, you can't create a user API key. You can still create and manage all other API keys. For example, service ID API keys. For more information, see the [FAQ about IAM](/docs/account?topic=account-iamfaq#tp-apikey).
{: note}


## Managing user API keys
{: #manage-user-keys}
{: ui}

To manage the {{site.data.keyword.cloud_notm}} API keys that are associated with your user identity or the ones that you have access to manage for other users in the account, go to **Manage** > **Access (IAM)** > **API keys** in the {{site.data.keyword.cloud_notm}} console. On the API keys page, you can create, edit, or delete {{site.data.keyword.cloud_notm}} API keys for yourself. You can also manage all [classic infrastructure API keys](/docs/account?topic=account-classic_keys) for users that you are an ancestor of in the user hierarchy. In addition, if you are the account owner or a user assigned the required access to manage other user's API keys in the account, you can use the **View** filter to list and manage those API keys too.

| Filter Options                                     | Displayed API Keys                                         | Required Access                            | Allowed Actions            |
|----------------------------------------------------|------------------------------------------------------------|--------------------------------------------|----------------------------|
| My {{site.data.keyword.cloud_notm}} API keys       | Your IBM Cloud API keys                                    | No access required                         | View, create, edit, delete |
| All user {{site.data.keyword.cloud_notm}} API keys | All IBM Cloud API keys created by all users in the account | Administrator role on IAM Identity service | View, edit, and delete     |
{: caption="Required access for API key management on the API keys page" caption-side="top"}

## Creating an API key in the console
{: #create_user_key}
{: help}
{: support}
{: ui}

As an {{site.data.keyword.cloud_notm}} user you might want to use an API key when you enable a program or script without distributing your password to the script. A benefit of using an API key is that a user or organization can create several API keys for different programs. The API keys can be deleted independently if compromised without interfering with other API keys or even the user. You can create up to 20 API keys.

To create an API key for your user identity in the UI, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**.
1. Click **Create an {{site.data.keyword.cloud_notm}} API key**.
1. Enter a name and description for your API key.
1. Click **Create**.
1. Then, click **Show** to display the API key. Or, click **Copy** to copy and save it for later, or click **Download**.

For security reasons, the API key is only available to be copied or downloaded at the time of creation. If the API key is lost, you must create a new API key.
{: tip}


## Creating an API key by using the CLI
{: #create_user_key-cli}
{: cli}

To create an API key by using the CLI, use the following command:

1. Enter `ibmcloud iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE] [--action-if-leaked VALUE]`, and specify a name, description, and file for saving your key. See the following example:

```bash
ibmcloud iam api-key-create MyKey -d "this is my API key" --file key_file --action-if-leaked "DELETE"
```
{: codeblock}

For `--action-if-leaked`, possible values are "NONE", "DISABLE", or "DELETE". The default action is "DISABLE".
- **DISABLE**: Disabling the key immediately blocks its ability to authenticate and access services. You can re-enable the key later if necessary.
- **DELETE**: The API key is permanently deleted from your account and can no longer be used to authenticate. This action cannot be undone.
- **NONE**: The key remains active and can still be used to access resources.

## Creating an API key by using the API
{: #create_user_key-api}
{: api}

To create an API key, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#create-api-key){: external} as shown in the following example:

```bash
curl -X POST 'https://iam.cloud.ibm.com/v1/apikeys' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -d '{
  "name": "My-apikey",
  "description": "my personal key",
  "iam_id": "IBMid-123WEREW",
  "account_id": "ACCOUNT_ID"
  "store_value": false
  "action_when_leaked": "delete"
  "support_sessions": false
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

For `action_when_leaked`, possible values are "none", "disable", or "delete". The default action is "disable".
- **disable**: Disabling the key immediately blocks its ability to authenticate and access services. You can re-enable the key later if necessary.
- **delete**: The API key is permanently deleted from your account and can no longer be used to authenticate. This action cannot be undone.
- **none**: The key remains active and can still be used to access resources.

For `support_sessions`, define whether you can manage CLI login sessions for the API key:
- **true**: Create login sessions for this API key, which you can manage by reviewing or revoking sessions. For more information, see [Monitoring your login sessions](/docs/account?topic=account-monitor-your-session).
- **false**: No sessions are created or tracked. You can't revoke or review any logins and you must delete or rotate the API key itself to block access.

## Before you begin
{: #before-you-begin-userapikey}
{: terraform}

Before you can manage user API keys by using Terraform, make sure that you complete the following steps:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

## Creating an API key by using Terraform
{: #create_user_key-api-terra}
{: terraform}

Use the following steps to create access groups by using Terraform.

1. Create an argument in your `main.tf` file. The following example creates an access group by using the `ibm_iam_api_key` resource, where `name` is a unique name to identify the API key.

   ```terraform
   resource "ibm_iam_api_key" "iam_api_key" {
    name        = "test1234"
   }
   ```
   {: codeblock}

   The `description` property is only available if a description is provided during API key creation. For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_api_key){: external} page.

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

## Updating an API key in the console
{: #update_user_key}
{: ui}

If you want to change the name or the description of an API key, complete the following steps in the UI or CLI.

To edit an API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**.
2. Identify the row of the API key that you want to update, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit**.
3. Update the information for your API key.
4. Click **Apply**.

To edit an API key that is not your own, but you have access to manage, go to the API keys page. Then, select the **All user {{site.data.keyword.cloud_notm}} API keys** option from the **View** menu to find the API key.
{: tip}


## Updating an API key by using the CLI
{: #update_user_key-cli}
{: cli}

To edit an API key by using the CLI, enter the following command:

1. Enter `ibmcloud iam api-key-update NAME [-n NAME] [-d DESCRIPTION]`, specifying the old name, new name, and new description for the key. For more information, see the following example:

```bash
ibmcloud iam api-key-update MyCurrentName -n MyNewName -d "the new description of my key"
```
{: codeblock}

## Updating an API key by using the API
{: #update_user_key-api}
{: api}

To edit an API key by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#update-api-key){: external} as shown in the following example:

```bash
curl -X PUT 'https://iam.cloud.ibm.com/v1/apikeys/APIKEY_UNIQUE_ID' -H 'Authorization: Bearer TOKEN' -H 'If-Match: <value of etag header from GET request>' -H 'Content-Type: application/json' -d '{
  "name": "My-apikey",
  "description": "my personal key"
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

## Updating an API key by using Terraform
{: #update_user_key-api-terra}
{: terraform}

Use the following steps to update an API key by using terraform:

1. In your Terraform configuration `main.tf` file, find the Terraform code that you used to create the `iam_api_key`.
1. The following example updates and API key by using the `ibm_iam_api_key` resource, where `name` is a unique name to identify the API key.

   ```terraform
   resource "ibm_iam_api_key" "iam_api_key" {
    name        = "test1234"
    description = "API key for users"
   }
   ```
   {: codeblock}

   The `description` property is only available if a description is provided during API key creation. For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_api_key){: external} page.

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

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_api_key).

## Locking and unlocking an API key in the console
{: #lock-user-key-ui}
{: ui}

For platform API keys that represent your user identity you can prevent the API key from being deleted by locking it. A locked API key has the **Locked** icon ![Locked icon](images/locked.svg "Locked").

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**.
2. Identify the row of the API key that you want to lock, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Lock**.

You can unlock your API key at any time to update or remove the API key from your account. Select the API key from the table that you want to unlock and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Unlock**.
{: tip}

## Locking and unlocking an API key by using the CLI
{: #lock-user-key-cli}
{: cli}

For platform API keys that represent your user identity you can prevent the API key from being deleted by locking it. To lock an API key, use the following command:

```bash
ibmcloud iam api-key-lock (NAME|UUID) [-f, --force]
```
{: codeblock}

**Prerequisites**:  Endpoint, Login

**Command options**:

NAME (required)
:   The name of the API key to lock, exclusive with UUID.

UUID (required)
:   UUID of the API key to lock, exclusive with NAME.

-f, --force
:   Forces lock without confirmation.



**Example**:

Lock API key `test-api-key`

```bash
ibmcloud iam api-key-lock test-api-key
```
{: codeblock}

To unlock an API key, run the following command:

```bash
ibmcloud iam api-key-unlock (NAME|UUID) [-f, --force]
```
{: codeblock}

**Prerequisites**:  Endpoint, Login

**Command options**:

NAME (required)
:   Name of the API key to be unlocked, exclusive with UUID.

UUID (required)
:   UUID of the API key to be unlocked, exclusive with NAME.

-f, --force
:   Forces unlock without confirmation.


**Example**:

Unlock API key `test-api-key`

```bash
ibmcloud iam api-key-unlock test-api-key
```
{: codeblock}

## Locking and unlocking an API key by using the API
{: #lock-user-key-api}
{: api}

For platform API keys that represent your user identity you can prevent the API key from being deleted by locking it.

### Locking an API key by using the API
{: #lock-keyapi}
{: api}

To lock an API key by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#lock-api-key){: external} as shown in the following example:

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
lock_api_key(self,
        id: str,
        **kwargs
    ) -> DetailedResponse

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
{: #unlock-keyapi}
{: api}

To unlock an API key by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api?code=go#unlock-api-key){: external} as shown in the following example:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/apikeys/APIKEY_UNIQUE_ID/lock' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
UnlockApiKeyOptions unlockApiKeyOptions = new UnlockApiKeyOptions.Builder()
    .id(apikeyId)
    .build();

service.unlockApiKey(unlockApiKeyOptions).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  id: apikeyId,
};

iamIdentityService.unlockApiKey(params)
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
response = iam_identity_service.unlock_api_key(id=apikey_id)

print(response)
```
{: codeblock}
{: python}

```go
unlockAPIKeyOptions := iamIdentityService.NewUnlockAPIKeyOptions(apikeyID)

response, err := iamIdentityService.UnlockAPIKey(unlockAPIKeyOptions)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

## Locking and unlocking an API key by using the Terraform
{: #lock-user-key-terra}
{: terraform}

For platform API keys that represent your user identity you can prevent the API key from being deleted by locking it.

### Locking an API key by using Terraform
{: #lock-keyapi-terra}
{: terraform}

Use the following steps to lock an API key by using Terraform:

1. In your Terraform configuration `main.tf` file, find the Terraform code that you used to create the `iam_api_key`.
1. The following example updates and API key by using the `ibm_iam_api_key` resource, where `entity_lock` indicates whether the API key is locked for further write operations. The default value is `false`.

   ```terraform
   resource "ibm_iam_api_key" "iam_api_key" {
    entity_lock        = "true"
   }
   ```
   {: codeblock}

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

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_api_key).


## Deleting an API key
{: #delete_user_key}
{: ui}

If you are using a key rotation strategy, you might want to delete an older key and replace it with a new key.

To delete an API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**.
2. Identify the row of the API key that you want to delete, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete**.
3. Then, confirm the deletion by clicking **Delete**.

To delete an API key that is not your own, but you have access to manage, go to the API keys page. Then, select the **All user {{site.data.keyword.cloud_notm}} API keys** option from the **View** menu to find the API key.
{: tip}

## Deleting an API key by using the CLI
{: #delete_user_key-cli}
{: cli}

To delete an API key by using the CLI:

Enter `ibmcloud iam api-key-delete NAME`, specifying the name of the key to delete.


## Deleting an API key by using the API
{: #delete_user_key-api}
{: api}

To delete an API key by using the API, call the [IAM Identity Service API](https://cloud.ibm.com/apidocs/iam-identity-token-api#delete-api-key){: external} as shown in the following example:

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

## Reviewing leaked user API keys by using the console
{: #review-apikeys-console}
{: ui}

If a leaked user API key is detected, you can use the console to review it. Complete the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}} console.
1. Select the account that contains the leaked API key.
1. Go to **Manage** > **Access** > **API keys** to review the leaked API key.

## Reviewing leaked user API keys by using the CLI
{: #review-apikeys-cli}
{: cli}

If a leaked user API key is detected, you can use the CLI to review it. Complete the following steps: 

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.
1. Select the account that contains the leaked API key.
1. Run the following command:

    ```bash
    ibmcloud iam api-key <API_key_ID>
    ```
    {: codeblock}
