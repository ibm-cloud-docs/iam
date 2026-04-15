---

copyright:

  years: 2015, 2026
lastupdated: "2026-04-15"

keywords: application programming interface key, API key, API, classic infrastructure API key, IBM Cloud API key, leaked API key, API key protection

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Understanding API keys
{: #manapikey}

An application programming interface key (API key) is a unique code that is passed in to an API to identify the calling application or user. API keys are used to track and control how the API is being used, for example to prevent malicious use or abuse of the API. The API key often acts as both a unique identifier and a secret token for authentication, and is assigned a set of access that is specific to the identity that is associated with it.
{: shortdesc}

To view your API keys, go to **Manage > Access (IAM) > API keys** in the {{site.data.keyword.cloud_notm}} console.

## {{site.data.keyword.cloud_notm}} API keys for users
{: #ibm-cloud-api-keys}

{{site.data.keyword.cloud}} API keys are associated with a user's identity. Each API key that a user creates has the same access that the user is assigned across all accounts where they are a member. Because the API key inherits all user access, it can provide the ability to access resources in any account where the user has permissions. For this reason, user API keys must be treated similarly to a username and password and must never be shared.

### Using functional IDs
{: #functional-ids}

{{site.data.keyword.cloud_notm}} API keys for users can be created and associated with a functional ID. A functional ID is a user ID created to represent a program, application, or service. The functional ID can be invited to an account and assigned only the access for a particular purpose, such as interacting with a specific resource or application.

If a service requires a user API key for interacting with other services or applications, use a functional ID user API key. By using the API key that is associated with the functional ID, you provide only the access that is needed for that service. Sharing a real user ID API key with a service allows the service to access any resources that the user can access across multiple accounts, which is highly discouraged.

Only the user for which the API key is associated and an Administrator for the IAM service can delete it. You can use {{site.data.keyword.cloud_notm}} API keys in the command-line interface (CLI) or as part of automation to log in as your user identity. You can also use {{site.data.keyword.cloud_notm}} API keys to access classic infrastructure APIs.

For more information about using an API key associated with your user identity, see [Managing user API keys](/docs/iam?topic=iam-userapikey#manage-user-keys).

## Other types of API keys
{: #othertypes}

In addition to your {{site.data.keyword.cloud_notm}} API keys, other types of API keys are available:

Service ID API keys
:   Service IDs are used to connect an application inside or outside of {{site.data.keyword.cloud_notm}} to an {{site.data.keyword.cloud_notm}} service. Service ID API keys inherit all access that is assigned to the specific service ID. For more information, see [Managing service ID API keys](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys).

Classic infrastructure API keys
:   Classic infrastructure API keys are used to call the APIs for classic infrastructure services. You can create only one classic infrastructure API key at a time. For more information, see [Managing classic infrastructure API keys](/docs/iam?topic=iam-classic_keys).

Service-specific API keys
:   Some services in {{site.data.keyword.cloud_notm}} might provide an API key when you work with the service. These are auto-generated API keys associated with a service ID. For example, if you are viewing the product details of a Watson service from the Resource list page, you can create a credential that includes an API key and secret that is specific to that service on the Service credentials page.

{{site.data.keyword.cloud_notm}} API keys can also be used to access classic infrastructure APIs.
{: tip}

## Understanding security best practices for API keys
{: #apikey-security-practices}

Implementing the following best practices for API keys can help to increase the security and safety of your workloads:

- Avoid embedding keys in code to minimize exposure risks.
- Rotate API keys regularly to limit the window of vulnerability. {{site.data.keyword.secrets-manager_short}} can help you automate this. For more information, see [Rotating your secrets](/docs/secrets-manager?topic=secrets-manager-manual-rotation).
- Apply the principle of least privilege when assigning permissions.
- Keep security contacts updated to receive timely notifications.
- Monitor {{site.data.keyword.atracker_short}} for suspicious API key usage.
- Set expiration dates on API keys when appropriate.

## Working with API keys
{: #work-with-apikeys}

To manage the {{site.data.keyword.cloud_notm}} API keys that are associated with your user identity or the ones that you have access to manage for other users in the account, go to **Manage > Access (IAM) > API keys** in the {{site.data.keyword.cloud_notm}} console.

On the {{site.data.keyword.cloud_notm}} API keys page, you can create, edit, or delete your own {{site.data.keyword.cloud_notm}} API keys. You can also manage all classic infrastructure API keys for users in your user hierarchy. If you are the account owner or a user with the required access to manage other user's API keys in the account, you can use the **View** filter to list and manage those API keys. 

### API key expiration
{: #apikey-expiration}

When an API key is created or updated, you can set an expiration date. If an expiration date is specified, the API key is invalid after that date. Expired API keys are automatically deleted 90 days after they expire. A few days before an API key expires, a notification is sent through the {{site.data.keyword.cloud_notm}} notification service to the user who owns the API key (for user-level keys) or to the account owner (for service ID API keys).

### Leaked API key protection
{: #leaked-apikey-protection}

API keys are powerful credentials that provide access to your {{site.data.keyword.cloud_notm}} resources and services. When these keys are inadvertently exposed in public repositories, logs, or other locations, they can create significant security risks. Bad actors actively scan public repositories for leaked credentials and can quickly exploit them for unauthorized access, crypto mining operations, or other malicious activities—often within minutes of exposure. Depending on the access granted to the user or service ID associated with the key, bad actors may be able to:

- Access or delete data.
- Provision resources in your account, including resources that may be used for bitcoin mining.
- Perform other actions in the services in your account.
- Create additional IDs or API keys within your account to give themselves persistent access - even after you rotate the compromised key.

{{site.data.keyword.cloud_notm}} leverages secret-scanning capabilities from platforms like GitHub and GitLab to help identify exposed API keys. When a key is determined to have been leaked, you or your security team can quickly take the appropriate action based on the disposition you configured for that key. Depending on your configuration, {{site.data.keyword.IBM_notm}} can take the following actions:

Disable the leaked key
:   The API key is immediately disabled by {{site.data.keyword.IBM_notm}}, preventing unauthorized use while you investigate and determine next steps. This approach is recommended for most keys except in situations where an assessment has been done and the risk due to an exposed key is low. If a key is disabled, your application's API calls to cloud services will fail, which could potentially cause an outage.

Delete the leaked key
:   The API key is permanently deleted by {{site.data.keyword.IBM_notm}} upon detection. This provides the strongest protection but requires creating a new key. If a key is deleted, your application's API calls to cloud services will fail, which could potentially cause an outage.

Do nothing
:   No automatic action is taken. You might still receive notifications about the exposure, but must manually address the issue.

Before you make a decision, it is important to weigh the security consequences of a key exposure against the consequences of an application outage. {{site.data.keyword.IBM_notm}} recommends using the "Disable" option for most keys except in situations where an assessment has been done and the risk if a key were exposed is low due to limited access. If your organization requires the "Do nothing" setting for specific API keys due to production requirements, {{site.data.keyword.IBM_notm}} encourages you regularly analyze your security posture, implement compensating controls such as frequent key rotation and plan to enable automatic protection when your environment allows.

For more information, see [Reviewing leaked user API keys](/docs/iam?topic=iam-userapikey&interface=ui#review-apikeys-console) or [Reviewing leaked service ID API keys](/docs/iam?topic=iam-serviceidapikeys&interface=ui#review-api-keys-serviceid-console).
 


## Required access for managing API keys
{: #API-key-access}

By default, you always have access to create your own API keys, and then update and delete them as needed. You can also manage your own classic infrastructure API key and any users' classic infrastructure API keys who you are an ancestor of in the classic infrastructure user hierarchy.

If the *Restrict API key creation* IAM account setting is enabled, then everyone in the account is blocked from creating API keys, including the account owner, unless they are assigned explicit access. For more information, see [Restricting users from creating API keys](/docs/iam?topic=iam-allow-api-create).
{: important}

If you are the account owner or a user with the required access, you can access other user's API keys or service ID API keys by using the **View** filter on the API keys page. You can edit or delete the API keys depending on your assigned access. You see only the filter options for the type of API keys that you have access to view and manage.

| Filter Options | Displayed API Keys | Required Access | Allowed Actions |
|-------------------|------------------|------------------|-------------|
| My {{site.data.keyword.cloud_notm}} API keys      | Your {{site.data.keyword.cloud_notm}} API keys | No access required | View, create, edit, delete |
| All {{site.data.keyword.cloud_notm}} user API keys | All {{site.data.keyword.cloud_notm}} API keys created by all users in the account | Administrator role on the IAM Identity service | View, edit, and delete |
| All service ID API keys | All API keys created for service IDs in the account | Administrator role on the IAM Identity service | View, edit, and delete |
| Classic infrastructure API keys | Your classic infrastructure API key and any classic infrastructure API keys for users who you are ancestor of in the user hierarchy | No access required other than being an ancestor in the user hierarchy | View details and delete |
{: caption="Table 1. Required access for API key management on the API keys page" caption-side="bottom"}
