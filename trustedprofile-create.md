---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: trusted profile, identity and access management, federated users, compute resources, IAM trusted profile, trust relationship, establish trust, trust policy, trusted entity, assume access, apply access, access group, service IDs, IBM Cloud services, CRN, cloud resource name, workload identity, without credentials

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}


# Trusted profiles for federated users and workloads
{: #create-trusted-profile}

Grant access without managing credentials. Use trusted profiles for federated users with SAML attributes or workload identities in compute resources.
{: shortdesc}

You can use trusted profiles to grant different {{site.data.keyword.cloud}} identities access to resources in your account. Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory. Or, use trusted profiles to set up fine-grained authorization for applications that are running in compute resources. This way, you aren't required to create service IDs or API keys for the compute resources. You can also establish trust with {{site.data.keyword.cloud_notm}} services or service IDs in another account to grant cross-account access.

A user doesn't need to be a member of the account to assume a trusted profile. A user can use the profile if the user's identity provider (IdP) matches an IdP used in the conditions of trust.

When you initially create a trusted profile, you can build conditions of trust with the following entity types: federated users, compute resources, service IDs, or {{site.data.keyword.cloud_notm}} services. After you create the trusted profile, you can add more conditions to combine multiple entity types in the same profile.

You can use {{site.data.keyword.cloudaccesstrailshort}} to monitor which federated users compute resources, service IDs, and {{site.data.keyword.cloud_notm}} services apply a trusted profile. For more information, see [Monitoring login sessions for trusted profiles](/docs/account?topic=account-trusted-profile-monitor).
{: tip}



## Before you begin
{: #tp-roles-reqs}

If you have the following access, you can create trusted profiles:

- Account owner
- Administrator role on all account management services
- Administrator role on the IAM Identity Service. For more information, see [IAM Identity service](/docs/account?topic=account-account-services#identity-service-account-management).

## Establishing trust with federated users in the console
{: #create-profile-federated-ui}
{: ui}

Complete the following steps to define which federated users can access specific resources:

1. [Enable authentication from an external identity provider](/docs/account?topic=account-ibm-idp-integration).
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Trusted profiles**.
1. Click **Create**.
1. Describe your profile by providing a name, email, and a description, then click **Continue**.

      In the email, you can either add a personal email ID or a distribution list.
      {: note}
      
      In the description, provide a list of actions available for this trusted profile.
      {: tip}

1. You can create the trusted profile before you add details by selecting **Decide later**. Or, establish trust by completing the following steps:
   1. Select **Federated users** as a trusted entity type from the list.<production>
   1. Select **Users federated by IBMid** or **Users federated by {{site.data.keyword.cloud_notm}} App ID** as the authentication method and input the default identity provider (IdP) you enabled in step 1.

      If the users that you are creating a trusted profile for use {{site.data.keyword.appid_full_notm}}, create the trusted profile as an App ID user, and likewise for IBMid. This way, your own SAML attributes can give you an idea of how to structure the trusted profile conditions. Other users with the same IdP can have different SAML attributes. Use your own attributes only as a hint. To use attributes in a claim that are different than your own, input them manually.
      {: tip}</production><idp>

      1. Select **Users federated by IBMid**, **Users federated by {{site.data.keyword.cloud_notm}} App ID**, or **Users federated by {{site.data.keyword.cloud_notm}} SAML** as the authentication method and input the default identity provider (IdP) you enabled in step 1.</idp>

   1. Add conditions based on your IdP data to define how and when federated users can apply the profile.
      * By clicking **Add a condition**, you can define multiple conditions. Federated users must meet all the conditions to be included in the trusted profile. For more information about the fields that are used to create conditions, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).
      * Click **View identity provider (IdP) data** to search attribute names and values in your own personal data from your IdP. For more information, see [Using IdP data to build trusted profiles](/docs/account?topic=account-ibm-idp-integration#trusted-profiles-idp-data).

   1. Define the session duration for how long a user can apply the profile before they must reauthenticate.

1. Click **Continue**.
1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-access).
1. Or, click **Create** without assigning any access.

For more information about the fields that are used to create conditions for trusted profiles, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).
{: tip}

## Establishing trust with compute resources in the console
{: #create-profile-compute}
{: ui}

Complete the following steps to set up better control over granting access to compute resources.

{{site.data.keyword.containerlong_notm}} supports only trusted profiles for versions 1.21 and newer. Free {{site.data.keyword.containerlong_notm}} clusters create only earlier versions. You have the choice to create clusters with an earlier version with the standard plan, so be sure to select version 1.21 or newer.
{: important}

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Trusted profiles**.
1. Click **Create profile**.
1. Describe your profile by providing a name and a description, and click **Continue**.
1. You can create the trusted profile before you add details by selecting **Decide later**. Or, establish trust by completing the following steps:
   1. Select **Compute resources** and select a compute service type from the list.
   1. If you select the option for **All service resources**, you can define multiple conditions to filter resources for the selected compute service type by clicking **Add a condition**. These conditions are based on attributes, such as resource groups or location, and apply to all existing and future resources. Resources must meet all the conditions to be included in the trusted profile.

      The Kubernetes namespace and service account names that you enter do not have to exist already. Any future namespaces or service accounts with these names can establish trust. To list existing namespaces, log in to your cluster and run `kubectl get ns`. To list existing service accounts, log in to your cluster and run `kubectl get sa -n <namespace>`. You can also enter `default` for both.
      {: tip}

   1. If you select **Specific resources**, you can establish trust with one or more existing compute resource instances directly without conditions. For example, a Kubernetes cluster.

1. Click **Continue**.
1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-access).
1. Or, click **Create** without assigning any access.

For more information about the fields that are used to create conditions for trusted profiles, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).
{: tip}

## Establishing trust with {{site.data.keyword.cloud_notm}} services in the console
{: #create-profile-services}
{: ui}

An {{site.data.keyword.cloud_notm}} service in your account or another account might need a token to run an operation in your account.

Example 1
:   A Project service instance in another account can assume a trusted profile to securely deploy an architecture in your account without the need for key rotation. For more information, see [Using trusted profiles to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-tp-project).

Example 2
:   A private catalog is an instance of the Catalog Management service that is identified by a CRN. You might want to validate products from your private catalog in an account that’s separate from the one that contains your catalog. You can give a private catalog access to create resources for validation in a target account by creating a trusted profile in the target account. Then you establish trust with the catalog by using the catalog CRN to link the service instance to the trusted profile. For more information, see [Setting up a target account for validation](/docs/account?topic=account-catalog-cross-validation).

Sharing resources across accounts by using trusted profiles works for a limited set of services and is not a general method for cross-account access for services.
{: note}

Complete the following steps to define how an {{site.data.keyword.cloud_notm}} service can access specific resources in your account:

1. Ask the administrator of the service for the Cloud Resource Name (CRN) that uniquely identifies the service instance. The CRN is used to authorize operations.

   The service administrator can find the CRN by going to the Navigation Menu icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Resource list** and clicking the name of the service that you're targeting. In the **Details** section, copy the CRN. For a private catalog CRN, go to **Manage** > **Catalogs** > **Private catalogs** and select the private catalog. **Click Actions...** > **Edit catalog details** to find the Catalog CRN.
   {: note}

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Trusted profiles**.
1. Click **Create profile**.
1. Define your profile by providing a name and a description, and click **Continue**.

   In the description, provide a list of actions that are available for the trusted profile.
   {: tip}

1. You can create the trusted profile before you add details by selecting **Decide later**. Or, establish trust by completing the following steps:
   1. Select **{{site.data.keyword.cloud}} services**.
   1. Enter the CRN that the service administrator provided to you.

   {{site.data.keyword.cloud_notm}} services are static identities that don't use conditions to establish trust. Instead, you establish trust by using the CRN to create a direct link with the trusted entity.
   {: note}

1. Click **Continue**.
1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-access).
1. Or, click **Create** without assigning any access.

## Establishing trust with service IDs in the console
{: #create-profile-serviceid}
{: ui}

You can use trusted profiles to give a service ID cross-account access and access to call classic infrastructure services. To give a service ID in one account access to a target account, create the trusted profile in the target account. Complete the following steps to define how a service ID can access specific resources in your account:

1. Ask an administrator in the other account for the service ID value that identifies the service ID.

   An administrator can find the service ID value by going to **Manage** > **Access (IAM)** > **Service IDs**, and selecting the service ID that you want to target. Click **Details** and copy the ID that begins with `ServiceId`.
   {: tip}

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Trusted profiles**.
1. Click **Create profile**.
1. Define your profile by providing a name and a description, and click **Continue**.

   In the description, provide a list of actions that are available for this trusted profile.
   {: tip}

1. You can create the trusted profile before you add details by selecting **Decide later**. Or, establish trust by completing the following steps:
   1. Select **Service IDs**
   1. Enter the service ID value that the administrator provided to you.
1. Click **Continue**.
1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui#tp-access).
1. Or, click **Create** without assigning any access.

Service IDs are static identities that don't use conditions to establish trust. Instead, you establish trust by using the ID value from the service ID's metadata to create a direct link with the trusted entity.
{: note}

## Assigning access to the trusted profile
{: #tp-access}
{: ui}

After you establish trust with federated users, compute resources, an {{site.data.keyword.cloud_notm}} service, or a service ID, you can assign access.

You can assign classic infrastructure access only if your account is linked to a Softlayer account.
{: note}

1. Assign access.
   * Assign access to the trusted profile by adding it to one or more access groups. This way, you can use the policies that exist in the access groups you've created.
      1. Select **Access groups** and select all the groups that you want to add the trusted profile to. You can assign users to only the access groups that you have access to manage.
      1. Click **Add**.
   * Assign access to the trusted profile with an access policy.
      1. Select **Access policy**. Based on your level of access, you can assign IAM policies and classic infrastructure permissions.
      1. Select a single service or a group of services, like **All Identity and Access enabled services**, **All Account Management services**, or **All IAM Account Management services**. Then, click **Next**.
      1. Scope the access to **All resources** or **Specific resources** based on selected attributes. Then, click **Next**.
      1. Select any combination of roles and permissions to define the scope of access, and click **Review**.
      1. Click **Add** to add your policy configuration to your summary.
      1. You can assign **Classic infrastructure** access by selecting a user, device, or service, then any combination of granular permissions.
1. Click **Create**.

## Establishing trust with federated users by using the CLI
{: #create-profile-federated-cli}
{: cli}

Complete the following steps to define which federated users can access specific resources:

1. [Enable authentication from an external identity provider](/docs/account?topic=account-ibm-idp-integration).
1. Create a trusted profile by running the following command:

   ```bash
   ibmcloud iam trusted-profile-create my-profile -d "sample trusted profile"
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_create).

1. To create conditions for your trusted profile, run the `ibmcloud iam trusted-profile-rule-create` command:

   ```bash
   ibmcloud iam trusted-profile-rule-create my-profile --name my-rule --type Profile-SAML --conditions claim:cn,operator:EQUALS,value:my_user --realm-name https://w3id.sso.ibm.com/auth/sps/samlidp2/saml20 --expiration 1200
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_rule_create).

1. Create an access policy with the `Viewer` role for all resources in the account by running the following command:

   ```bash
   ibmcloud iam trusted-profile-policy-create --roles Viewer
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create).

## Establishing trust with compute resources by using the CLI
{: #create-profile-compute-cli}
{: cli}

Complete the following steps to set up better control over granting access to compute resources.

{{site.data.keyword.containerlong_notm}} supports only trusted profiles for versions 1.21 and newer. Free {{site.data.keyword.containerlong_notm}} clusters create only earlier versions. You have the choice to create clusters with an earlier version with the standard plan, so be sure to select version 1.21 or newer.
{: important}

1. Create a trusted profile by running the following command:

   ```bash
   ibmcloud iam trusted-profile-create sample-compute-profile -d "sample trusted profile for compute resources"
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_create).

1. Create conditions for your trusted profile by using the `ibmcloud iam trusted-profile-rule-create` command:

   ```bash
   ibmcloud iam trusted-profile-rule-create sample-compute-profile --name cr-rule --type Profile-CR --conditions claim:namespace,operator:EQUALS,value:default --conditions claim:crn,operator:EQUALS,value:crn:test:bluemix:public:containers-kubernetes:us-south:a/test:: --cr-type IKS_SA
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_rule_create).

   You can also create a direct link:

   ```bash
   ibmcloud iam trusted-profile-link-create sample-compute-profile --name my_link --cr-type IKS_SA --link-name default  --link-namespace default --link-crn my_compute_resource_crn
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_link_create).

1. Create an access policy by running the following command:

   ```bash
   ibmcloud iam trusted-profile-policy-create --roles Viewer
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create).

## Establishing trust with {{site.data.keyword.cloud_notm}} services by using the CLI
{: #create-profile-services-cli}
{: cli}

An {{site.data.keyword.cloud_notm}} service in another account might need a token to execute an operation in your account. Complete the following steps to define how an {{site.data.keyword.cloud_notm}} service can access specific resources in your account:
1. Ask the administrator on the service in another account for the CRN that uniquely identifies the service instance. The CRN is used to authorize operations.

   The service administrator can find the CRN by going to the Navigation Menu icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Resource list** and clicking the service that you're targeting. In the **Details** section, copy the CRN.
   {: note}

1. Create the trust relationship with a direct link:
   ```bash
   ibmcloud iam trusted-profile-link-create sample-cloudservice-profile --name my_cloudservice_link --link-crn `crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource`
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_link_create).
1. Create an access policy by running the following command:
   ```bash
   ibmcloud iam trusted-profile-policy-create --roles Viewer
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create).

## Establishing trust with service IDs by using the CLI
{: #create-profile-serviceid-cli}
{: cli}

Complete the following steps to define how a service ID can access specific resources in your account:

You can use trusted profiles to give a service ID cross-account access and access to call Classic Infrastructure services.
{: tip}

1. Ask an administrator in the other account for the service ID value that identifies the service ID.

   An administrator can find the service ID value by going to **Manage** > **Access (IAM)** > **Service IDs** and selecting the service ID that you want to target. Click **Details** and copy the ID that begins with `ServiceId`.
   {: note}

1. Create the trust relationship with a direct link:
   ```bash
   ibmcloud iam trusted-profile-link-create sample-serviceid-profile --name my_serviceid_link --link-crn `crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource`
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_link_create).
1. Create an access policy by running the following command:
   ```bash
   ibmcloud iam trusted-profile-policy-create --roles Viewer
   ```
   {: codeblock}

   For more information, see the [CLI reference](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create).

## Assigning access to the trusted profile by using the CLI
{: #tp-access-cli}
{: cli}

After you establish trust with federated users, compute resources, an {{site.data.keyword.cloud_notm}} service, or a service ID, you can assign access.

You can assign classic infrastructure access only if your account is linked to a Softlayer account.
{: note}

Use the command [`trusted-profile-policy-create`](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create) to assign an access policy to the trusted profile. The following example assigns a policy with the Administrator role on **All Account Management services**:

```bash
ibmcloud iam trusted-profile-policy-create Profile-36f5c562-1t36-4442-b7f0-2663c85386f1 --roles Administrator --attributes serviceType=service
```
{: codeblock}
{: curl}

## Establishing trust with federated users by using the API
{: #create-profile-federated-api}
{: api}

Complete the following steps to define which federated users can access specific resources:

1. [Enable authentication from an external identity provider](/docs/account?topic=account-ibm-idp-integration).
1. Create a trusted profile by specifying your account ID.

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/v1/profiles' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
   "name": "My Nice Profile",
   "description": "My Nice Profile - desc",
   "account_id": "ACCOUNT_ID"
   }'
   ```
   {: codeblock}

   In the description, provide a list of actions available for this trusted profile.
   {: tip}

1. Create conditions for your trusted profile. For federated users, set the `type` attribute to `Profile-SAML`. The `realm-name` is the IdP URL. For more information, see the [IAM Identity Services API](/apidocs/iam-identity-token-api).

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID/rules' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
   "type": "Profile-SAML",
   "realm_name": "https://www.example.org/my-nice-idp",
   "expiration": 43200,
   "conditions": [
   {
   "claim": "groups",
   "operator": "EQUALS",
   "value": "\"cloud-docs-dev\""
      }
      ]
   }'
   ```
   {: codeblock}

   There is a limit of 20 claim rules per trusted profile.
   {: note}

1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=api#tp-access-api).

## Establishing trust with compute resources with the API
{: #create-profile-compute-api}
{: api}

Complete the following steps to set up better control over granting access to compute resources.

{{site.data.keyword.containerlong_notm}} supports only trusted profiles for versions 1.21 and newer. Free {{site.data.keyword.containerlong_notm}} clusters create only earlier versions. You have the choice to create clusters with an earlier version with the standard plan, so be sure to select version 1.21 or newer.
{: important}

1. Create a trusted profile by specifying your account ID.

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/v1/profiles' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
   "name": "My Nice Profile",
   "description": "My Nice Profile - desc",
   "account_id": "ACCOUNT_ID"
   }'
   ```
   {: codeblock}

   In the description, provide a list of actions available for this trusted profile.
   {: tip}

1. Create a claim rule for your trusted profile that follows the principle of least privilege by specifying conditions that target only the resources that need access. Conditions apply to all existing future resources. You can also create a direct link with specific, existing resources.

      Create conditions
      :   For compute resources, set the `type` attribute to `Profile-CR`. For more information, see the [IAM Identity Services API](/apidocs/iam-identity-token-api#create-claim-rule).

      ```bash
      curl -X POST 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID/rules' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
      "type": "Profile-CR",
      "conditions": [
      {
      "claim": "namespace",
      "operator": "EQUALS",
      "value": "\"default123\""
         }
         ]
      }'
      ```
      {: codeblock}

      There is a limit of 20 claim rules per trusted profile.
      {: note}

      Create a direct link
      :   You can establish a direct link with specific, existing resources.
      ```bash
      curl -X POST 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID/links' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
         "name": "my link",
         "cr_type": "VSI",
         "is_cross_account": true,
         "link": {
      "crn": "crn:v1:staging:public:iam-identity::a/18e3020749ce4744b0b472466d61fdb4::computeresource:Fake-Compute-Resource",
      "namespace": "default",
      "name": "my compute resource name"
         }
      }'
      ```
      {: codeblock}

1. (Optional) [Assign access to the trusted profile](/docs/account?topic=account-create-trusted-profile&interface=api#tp-access-api).

## Assigning access to the trusted profile by using the API
{: #tp-access-api}
{: api}

After you establish trust with federated users, compute resources, an {{site.data.keyword.cloud_notm}} service, or a service ID, you can assign access.

You can assign classic infrastructure access only if your account is linked to a Softlayer account.
{: note}

The following example assigns a policy with the Administrator role on **All Account Management services**:

```bash
curl -X POST \
'https://iam.cloud.ibm.com/v1/policies' \
-H 'Authorization: $TOKEN'\
-H 'Content-Type: application/json'\
-d '{
  "type": "access",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "Iam-Profile-35f55552-1e36-4442-z7f0-2673c85386f9"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:iam::::role:Administrator"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceType",
          "value": "platform-service"
        }
      ]
    }
  ]
}'
```
{: curl}
{: codeblock}

```java
SubjectAttribute subjectAttribute = new SubjectAttribute.Builder()
        .name("iam_id")
        .value("Iam-Profile-35f55552-1e36-4442-z7f0-2673c85386f9")
        .build();

PolicySubject policySubjects = new PolicySubject.Builder()
        .addAttributes(subjectAttribute)
        .build();

PolicyRole policyRoles = new PolicyRole.Builder()
        .roleId("crn:v1:bluemix:public:iam::::role:Administrator")
        .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
        .name("accountId")
        .value("exampleAccountId")
        .operator("stringEquals")
        .build();

ResourceAttribute serviceTypeResourceAttribute = new ResourceAttribute.Builder()
        .name("serviceType")
        .value("platform-service")
        .operator("stringEquals")
        .build();

PolicyResource policyResources = new PolicyResource.Builder()
        .addAttributes(accountIdResourceAttribute)
        .addAttributes(serviceTypeResourceAttribute)
        .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
        .type("access")
        .subjects(Arrays.asList(policySubjects))
        .roles(Arrays.asList(policyRoles))
        .resources(Arrays.asList(policyResources))
        .build();

Response<Policy> response = service.createPolicy(options).execute();
Policy policy = response.getResult();

System.out.println(policy);
```
{: java}
{: codeblock}

```javascript
const policySubjects = [
  {
    attributes: [
      {
        name: 'iam_id',
        value: "Iam-Profile-35f55552-1e36-4442-z7f0-2673c85386f9",
      },
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:iam::::role:Administrator',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: 'exampleAccountId',
  operator: 'stringEquals',
};
const serviceTypeResourceAttribute = {
  name: 'serviceType',
  value: 'platform-service',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceTypeResourceAttribute]
  },
];
const params = {
  type: 'access',
  subjects: policySubjects,
  roles: policyRoles,
  resources: policyResources,
};

iamPolicyManagementService.createPolicy(params)
  .then(res => {
    examplePolicyId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
policy_subjects = PolicySubject(
  attributes=[SubjectAttribute(name='iam_id', value='Iam-Profile-35f55552-1e36-4442-z7f0-2673c85386f9')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:iam::::role:Administrator')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
  name='serviceType', value='platform-service')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_type_resource_attribute])

policy = iam_policy_management_service.create_policy(
  type='access',
  subjects=[policy_subjects],
  roles=[policy_roles],
  resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
  Name:  core.StringPtr("iam_id"),
  Value: core.StringPtr("Iam-Profile-35f55552-1e36-4442-z7f0-2673c85386f9"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:iam::::role:Administrator"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr("ACCOUNT_ID"),
  Operator: core.StringPtr("stringEquals"),
}
serviceTypeResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceType"),
  Value:    core.StringPtr("platform-service"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceTypeResourceAttribute},
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
  "access",
  []iampolicymanagementv1.PolicySubject{*policySubjects},
  []iampolicymanagementv1.PolicyRole{*policyRoles},
  []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}


