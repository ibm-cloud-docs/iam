---

copyright:

  years: 2022, 2026
lastupdated: "2026-03-20"

keywords: what is IAM, IAM features, IAM API, how IAM works, federated users, service IDs, trusted profiles, workload identity

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Identity types for users, services, and workloads
{: #identity-overview}

IBM Cloud supports multiple identity types including federated users, service IDs, trusted profiles, and API keys for secure workload authentication.
{: shortdesc}

The identity concept consists of user identities, service and app identities, API keys for users and service IDs, trusted profiles, and resource identities. Users are identified by their IBMid, SoftLayer ID, {{site.data.keyword.appid_short}} user ID, or federated user attributes.

{{site.data.keyword.cloud_notm}} IAM grants access to individual identities or a group of identities by using policies. The policies allow for users to grant access while adhering to the principle of least privilege by utilizing roles and scoped resources. Except for account owners, user identities do not have any access grants by default. Each access grant is independent of other access grants, and users with permission can access resources by using the console and APIs. The actions that are allowed can be for a single API or a group of APIs depending on customer needs. Access can be granted at a high level for a grouping of resources or scoped to a single resource depending on customer needs.

Removing access for inactive identities can reduce the risk of unauthorized access to your {{site.data.keyword.cloud_notm}} resource and help you manage access more efficiently. For more information, see [Identifying inactive identities](/docs/account?topic=account-id-inactive-identities).
{: tip}

## Users
{: #users-bestpract}

User IDs are best used when a person needs a digital identity in an account. Users are invited to the account and given access to the resources in the account. Users log in by using their IBMid, SoftLayer ID, {{site.data.keyword.appid_short}} user ID, or federated user ID. Each user is also identified by a generated ID called an IAM ID.

IAM IDs always include a realm to identify the provider of the user, such as IBMid or an external identity provider. In the IAM ID, the realm is followed by a series of numbers that is a unique identifier. For example, the IAM ID for a user with an IBMid would look like `IBMid-20000AB1C`.

IAM IDs are most commonly used when you assign access to others by using the API. They are used to identify a user, service ID, trusted profile, or resource. The IAM ID is included in the token when used in the console, CLI, or API. Access policies are defined by using IAM IDs since it is the identity that can be verified in the IAM token.

To find your IAM ID, go to **Manage** >  **Access (IAM)**. You can see your IAM ID in the My user details section. To view other users' IAM IDs, go to **Manage** > **Access (IAM)** > **Users**, then select a user's name from the list and click **Details**.

### User API keys
{: #user-api-key}

{{site.data.keyword.cloud_notm}} API keys are credentials that are associated with a user's identity. The access that the user is assigned can be from policies across multiple accounts that the user is a member of. User API key credentials can be used to make API and CLI calls. The user API key can be used directly or used to generate a token.

For more information about using an API key associated with your user identity, see [Managing user API keys](/docs/account?topic=account-userapikey).

{{_include-segments/federating-segment.md}}

### Functional IDs
{: #functionalid-bestpract}

Functional IDs are most commonly used when an application or service needs a digital identity and access to IAM-enabled resources or Classic infrastructure resources. Some services require a functional ID when you create service instances, for example the {{site.data.keyword.containershort}}.

A functional ID is a type of user ID that exists in your Identity Provider's (IdP) user directory, but it's not tied to a specific user. To create a functional ID, you must create a new user in the user directory and invite them to your {{site.data.keyword.cloud_notm}} account.

The functional ID is used to create service instances, like {{site.data.keyword.containershort}} clusters. This way, instances aren't linked to a specific person that might leave the company, which would leave the instance without an owner. Generally, functional IDs can do more in {{site.data.keyword.cloud_notm}} than a service ID. For example, functional IDs, like user IDs, can be granted access to services and applications through access policies.

{{site.data.keyword.cloud_notm}} API keys for users can be created and associated with a functional ID. If a service requires a user API key for interacting with other services or applications, use the functional ID API key. By using the API key that is associated with the functional ID, you can provide only the access that is needed for that service.

If you're using a functional ID as the account owner, instead consider [Setting an alternative account owner](/docs/account?topic=account-transfer&interface=ui#grant-alt-owner). This is available only for classic infrastructure accounts.
{: tip}

## Service IDs
{: #serviceid-bestpract}

Service IDs are another type of identity that is used in an account. Service IDs are used to provide a separate identity for services and applications. Service IDs are best used when an application or service needs a digital identity and needs access to only IAM-enabled resources. You can create a service ID to be used by an application that needs access to your {{site.data.keyword.cloud_notm}} services so that individual user credentials don't need to be used.

### Service ID API keys
{: #serviceid-api-key}

You can also create API keys that are associated with service IDs to authenticate applications as a particular service ID. This way, the applications can access resources that are assigned to that specific service ID. Service ID API key credentials can be used to make API and CLI calls. For more information about creating API keys associated with a service ID, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys#serviceidapikeys).

## Trusted profiles
{: #trustedprofiles-bestpract}

Similar to other identities within IAM, trusted profiles are treated as a subject that is granted access in IAM policies.

Usually, for a user to take an action on a resource within an account, that identity must explicitly be added to the account. With trusted profiles, it is possible for a user to complete the actions without being invited to an account. Instead, they are automatically granted access to resources when they apply the trusted profile identity during login. Only users federated by an external IdP can be mapped to trusted profiles during login by evaluating SAML-based attributes to determine which profiles their identity can apply.

Similarly, instead of creating a service ID, generating an API key, and getting the application to store and validate that key, you can create [trusted profiles for compute resources](/docs/account?topic=account-create-trusted-profile) to define fine-grained authorization for all applications that are running in a compute resource. Compute resources become identities when used as part of a trusted profile. Trust with compute resources is established by conditions based on resource attributes, or creating a direct link to a specific resource.

You can also [establish trust with {{site.data.keyword.cloud_notm}} services](/docs/account?topic=account-create-trusted-profile&interface=ui#create-profile-services) that need to run an operation in your account. Or, use trusted profiels to give a [service ID](/docs/account?topic=account-create-trusted-profile&interface=ui#create-profile-serviceid) from another account access in your account.

## Resource identities
{: #resources-bestpract}

The final piece of the identity concept in IAM is {{site.data.keyword.cloud_notm}} resources, which are identified by their [cloud resource names](#x9494304){: term} (CRN). All resources that are created from the catalog are identified by their CRN. These CRNs are used for service-to-service authorizations in IAM. Additionally, you use a CRN to assign access to specific resources when you use the API. For more information, see [Cloud Resource Names](/docs/account?topic=account-crn) and [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth).


For more information, see [Cloud Resource Names](/docs/account?topic=account-crn) and [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth).
