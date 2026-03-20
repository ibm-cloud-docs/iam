---

copyright:

  years: 2015, 2026
lastupdated: "2026-03-20"

keywords: application programming interface key, API key, API, classic infrastructure API key, IBM Cloud API key

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Understanding API keys
{: #manapikey}

An application programming interface key (API key) is a unique code that is passed in to an API to identify the calling application or user. API keys are used to track and control how the API is being used, for example to prevent malicious use or abuse of the API. The API key often acts as both a unique identifier and a secret token for authentication, and is assigned a set of access that is specific to the identity that is associated with it.
{: shortdesc}

To view your API keys, go to **Manage** > **Access (IAM)** > **API keys** in the {{site.data.keyword.cloud_notm}} console.

## {{site.data.keyword.cloud_notm}} API keys for users
{: #ibm-cloud-api-keys}

{{site.data.keyword.cloud}} API keys are associated with a user's identity, and each API key that a user creates has the same access that the user is assigned. The access that the user is assigned can be from policies across multiple accounts that the user is a member of. Therefore, it is possible that a user's API key can be used to generate a token and access resources that a user has access to, outside of the account where the API key was created.

The user API key can be used directly or used to generate a token. Because users can be members of multiple accounts and have access to many resources across multiple accounts, and the API key is used to identify the user, it can provide the ability to gain access to almost any resource, in any account, that the user has access to. For this reason, the user API key must be treated similarly to a username and password and should never be shared.

{{site.data.keyword.cloud_notm}} API keys for users can be created and associated with a functional ID. A functional ID is a user ID created to represent a program, application, or service. The functional ID can be invited to an account and assigned only the access for a particular purpose, such as interacting with a specific resource or application. The functional ID must be granted only the minimum level access in a single account that is needed for the specific function that it was created.

If a service requires a user API key for interacting with other services or applications, use the functional ID user API key. By using the API key that is associated with the functional ID, you can provide only the access that is needed for that service. Sharing a real user ID API key with a service allows the service to access any resources that the user can access across multiple accounts. Sharing a real user ID API key is highly discouraged.

Only the user for which the API key is associated and an Administrator for the Identity Service can delete it. You can use the {{site.data.keyword.cloud_notm}} API keys in the command-line interface (CLI) or as part of automation to log in as your user identity. You can also use {{site.data.keyword.cloud_notm}} API keys to access classic infrastructure APIs. 

For more information about using an API key associated with your user identity, see [Managing user API keys](/docs/account?topic=account-userapikey#manage-user-keys).


## Other types of API keys
{: #othertypes}

In addition to your {{site.data.keyword.cloud_notm}} API keys, a couple of other types of API keys are available that you might use:

* Service ID API keys
* Classic infrastructure API keys
* Service-specific API keys

You can also use API keys that are associated with service IDs that you create. Service IDs are used to connect an application inside or outside of {{site.data.keyword.cloud_notm}} to an {{site.data.keyword.cloud_notm}} service. Service ID API keys inherit all access that is assigned to the specific service ID. For more information about creating API keys associated with a service ID, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys#serviceidapikeys).

[Classic infrastructure API keys](/docs/account?topic=account-classic_keys) are used to call the APIs for classic infrastructure services. You can create only one classic infrastructure API key at a time. You can create a classic infrastructure API key for yourself from the API keys page or the User details page.

{{site.data.keyword.cloud_notm}} API keys can also be used to access classic infrastructure APIs.
{: tip}

Some services in {{site.data.keyword.cloud_notm}} might provide an API key when you work with the service that is an auto-generated API key associated with a service ID. For example, if you are viewing the product details of a Watson service by going to the Resource list page, you can create a credential that includes an API key and secret that is specific to that service on the Service credentials page.

## Working with API keys
{: #work-with-apikeys}

To manage the {{site.data.keyword.cloud_notm}} API keys that are associated with your user identity or the ones that you have access to manage for other users in the account, go to **Manage** &gt; **Access (IAM)** &gt; **API keys** in the {{site.data.keyword.cloud_notm}} console.

On the {{site.data.keyword.cloud_notm}} API keys page, you can create, edit, or delete {{site.data.keyword.cloud_notm}} API keys for yourself, and you can manage all classic infrastructure API keys for users to which you are an ancestor in the user hierarchy. This means that you can manage API keys for all users you invited to the account, or your child users invited to the account, and so on. In addition, if you are the account owner or a user with the required access to manage other user's API keys in the account, you can use the **View** filter to list and manage those API keys.

When an API key is created or updated, users can set an expiration date. If an expiration date is specified, the API key is invalid after that date.



When an API key is created or updated, users can set an expiration date. If an expiration date is specified, the API key is invalid after that date. Expired API keys are automatically deleted 90 days after expiration.

A few days before an API key expires, a notification is sent through the {{site.data.keyword.cloud_notm}} notification service to the user who owns the API key (for user-level keys) or to the account owner (for service ID API keys).

Users and account administrators are notified through {{site.data.keyword.cloud_notm}} notification service if an API key is leaked. When you create an API key, you can specify what action must be taken if the key is compromised. You can select from the following actions:

- Do nothing
- Disable the API key
- Delete the API key

For more information on reviewing leaked user API keys, see [Reviewing leaked user API keys by using the console](/docs/account?topic=account-userapikey&interface=ui#review-apikeys-console) and [Reviewing leaked user API keys by using the CLI](/docs/account?topic=account-userapikey&interface=cli#review-apikeys-cli) respectively.

For more information on reviewing leaked service ID API keys, see [Reviewing leaked service ID API keys by using the console](/docs/account?topic=account-serviceidapikeys&interface=ui#review-api-keys-serviceid-console) and [Reviewing leaked service ID API keys by using the CLI](/docs/account?topic=account-serviceidapikeys&interface=cli#review-api-keys-serviceid-cli) respectively.

### Required access for managing API keys
{: #API-key-access}

By default, you always have access to create your own API keys, and then update and delete them as needed. You can also manage your own classic infrastructure API key and any users' classic infrastructure API keys who you are an ancestor of in the classic infrastructure user hierarchy, meaning that you invited the user or someone you invited to the account invited the user, and so on.

If the Restrict API key creation IAM account setting is enabled, then everyone in the account is blocked from creating API keys, including the account owner, unless they are assigned explicit access. For more information, see [Restricting users from creating API keys](/docs/account?topic=account-allow-api-create).
{: important}

If you are the account owner or a user with the required access, you can access other user's API keys or service ID API keys by using the **View** filter on the API keys page. You can edit or delete the API keys depending on your assigned access. You see only the filter options for the type of API keys that you have access to view and manage.

| Filter Options | Displayed API Keys | Required Access | Allowed Actions |
|-------------------|------------------|------------------|-------------|
| My {{site.data.keyword.cloud_notm}} API keys      | Your {{site.data.keyword.cloud_notm}} API keys | No access required | View, create, edit, delete |
| All {{site.data.keyword.cloud_notm}} user API keys | All {{site.data.keyword.cloud_notm}} API keys created by all users in the account | Administrator role on the IAM Identity service | View, edit, and delete |
| All service ID API keys | All API keys created for service IDs in the account | Administrator role on the IAM Identity service | View, edit, and delete |
| Classic infrastructure API keys | Your classic infrastructure API key and any classic infrastructure API keys for users who you are ancestor of in the user hierarchy | No access required other than being an ancestor in the user hierarchy | View details and delete |
{: caption="Required access for API key management on the API keys page" caption-side="top"}


