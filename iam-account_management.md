---

copyright:

  years: 2019, 2026
lastupdated: "2026-03-20"

keywords: account management, access, access policy, account administrator, user management, account management services, use account management services to grant users in the account access to invite users to the account, billing service, support center service, identity service, global catalog service, enterprise service, license service, entitlement service, license and entitlement service, access management service, catalog management service, cloud shell service, software instance service

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Assigning access to account management services
{: #account-services}

As the account owner or the administrator of an account management service, you can grant users access to invite users to the account, track billing and usage, and work with support cases. Users with account management access policies can also manage service IDs, access policies, catalog entries, access groups, resources for the {{site.data.keyword.compliance_short}} service, and work with Context-based restrictions.
{: shortdesc}





## Assigning access in the console
{: #console-acct-mgmt}
{: ui}

To assign access to one or all account management services, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and then select **Users**.
1. Click the user that you want to assign access, then go to **Access** > **Assign access**.
1. For the service, select **All Account Management services** or select a specific account management service. Then, click **Next**.
1. Scope the access to **All resources** or **Specific resources**. Then, click **Next**.
1. Select any combination of roles or permissions, and click **Review**.
1. Click **Add** to add your policy configuration to your policy summary.
1. Click **Assign**.

To grant another user full access to the account for the purposes of managing user access and all IAM-enabled account resources, you must assign two policies. To create the first policy, select **All Identity and Access enabled services** with the Administrator platform role and Manager service role. To create the second policy, select **All Account Management services** with the Administrator role assigned.

Users with the Administrator role for account management services can change the access of other users and remove users from the account, including other users with the administrator role.
{: important}

## Actions and roles for account management services
{: #account-management-actions-roles}
{: ui}

The following tables outline the actions that users can take when they are assigned a specific role for each account management service. Review the information to ensure that you are assigning the correct level of access to your users.

### All Account Management services
{: #all-account-management}

To quickly give users a wide range of account management access, you can assign a policy on all account management services. When a user is assigned a role on **All Account Management services**, they can complete all of the actions that are associated with that role for each individual service.

Give users access to the group of **All Account Management services** so that they can work with the following services:

- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role management
- User Management
- Billing
- Catalog management
- Context-based restrictions
- Enterprise
- Global catalog
- IBM Cloud shell settings
- License and entitlement
- Partner Center
- Partner Center - Sell
- Projects
- Security and Compliance Center
- Software instance
- Support center

| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for the account management services                                                  |
| Operator      | All operator role actions for the account management services                                                |
| Editor        | All editor role actions for the account management services and the ability to create resource groups        |
| Administrator | All administrator role actions for the account management services and the ability to create resource groups |
{: caption="Roles and example actions for a policy on all account management services" caption-side="top"}


### All IAM Account Management services
{: #all-iam}

Identity and Access Management (IAM) services make up a subset of all account management services. Give users access to the group of **All IAM Account Management services** so that they can work with the following services:

- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role Management
- User Management


| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for IAM services                                                  |
| Operator      | All operator role actions for IAM services                                                |
| Editor        | All editor role actions for IAM services and the ability to create resource groups        |
| Administrator | All administrator role actions for IAM services and the ability to create resource groups |
| User API key creator | Create API keys when the account setting to restrict API key creation is enabled |
| Service ID creator | Create service IDs when the account setting to restrict service ID creation is enabled |
| Template Administrator | Create enterprise IAM templates for access groups, trusted profiles, account settings, and policies. This role is available in only the root enterprise account. |
| Template Assignment Administrator | Assign enterprise IAM templates to child accounts. This role is available in only the root enterprise account. |
{: caption="Roles and example actions for a policy on all IAM account management services" caption-side="top"}

Some roles that you might assign on a policy for **All IAM Account Management services** affect only certain resources. For example, the role Service ID Creator is relevant to only the IAM Identity service.
{: note}

### Billing
{: #billing-acct-mgmt}

You can give users access to update account settings, view subscriptions, view offers, apply subscription and feature codes, update spending limits, and track usage by using the Billing service.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        | View account feature settings   \n  \n View subscriptions in account   \n  \n View account name   \n  \n View subscription balances and track usage           |
| Operator      | View account feature settings   \n  \n View subscriptions in account   \n  \n View and change account name |
| Editor        | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage |
| Administrator | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage   \n  \n Create an enterprise |
{: caption="Roles and example actions for the Billing service" caption-side="top"}

It's possible to view subscription balances and usage from the Account settings page, but you can't view the Account settings page with the Viewer or Operator roles. To access the Account settings page and your subscription information from that page, you need the Editor role or higher.
{: note}

### Catalog management
{: #catalog-management-account-management}

You can give users access to view private catalogs and catalog filters, create private catalogs, add software to private catalogs, and set catalog filters.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View account-level filters set for the {{site.data.keyword.cloud_notm}} catalog   \n  \n View private catalogs                                          |
| Operator      | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters    |
| Editor        | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters |
| Administrator | Set account-level filters for the {{site.data.keyword.cloud_notm}} catalog   \n  \n Create, update, and delete private catalogs   \n  \n Publish {{site.data.keyword.IBM_notm}}-approved products   \n  \n Assign access policies |
| Publisher     | Publish products that are approved by {{site.data.keyword.IBM_notm}} from a private catalog |
{: caption="Roles and example actions for the catalog management service" caption-side="top"}

### Context-Based Restrictions
{: #cbr-account-management}

You can give users access to view, create, update, and remove network zones. To create a context-based restriction rule for a service, you must be assigned an IAM policy with the Administrator role the service you are creating a rule against. For example, if you want to create a rule to protect a **Key Protect** instance, you must be assigned the Administrator role on the **Key Protect** service and the Viewer role or higher on the **Context-based restrictions** service.

The Viewer role on the Context-based restrictions service allows you to add network zones to your rule.
{: note}

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View network zones|
| Editor        | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones  |
| Administrator | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones |
{: caption="Roles and example actions for the context-based restrictions service" caption-side="top"}

### Enterprise
{: #enterprise-account-management}

You can use the Enterprise service to assign users access to manage an enterprise by creating accounts within the enterprise, assigning accounts to account groups, naming account groups, and more. This type of policy works only if it is assigned within the enterprise account.

| Roles               | Actions                                                                                                                                    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer              | View the enterprise, account groups, and accounts                                                                                          |
| Operator            | Not applicable                                                                                          |
| Editor              | View and update the enterprise name and domain, create accounts and account groups, view usage reports, and import accounts. |
| Administrator       | View and update the enterprise name and domain, create accounts and account groups, move accounts between account groups, import existing accounts, and view usage reports |
| Usage report viewer | View the enterprise, accounts, and account groups and view usage reports for all accounts in the enterprise.                               |
{: caption="Roles and example actions for the Enterprise service" caption-side="top"}

### Global catalog
{: #global-catalog-account-management}

You can give users access to view private products in the catalog or change the visibility of private products for other users in the account.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View private services                                                                                  |
| Operator      | View private services                                                                                  |
| Editor        | Change object metadata but can't change visibility for private services                                |
| Administrator | Change object metadata or visibility for private services, and restrict visibility of a public service |
{: caption="Roles and example actions for the Global Catalog service" caption-side="top"}

### IAM Access Groups
{: #access-groups-account-management}

You can give users access to view, create, edit, and delete access groups in the account by using the IAM Access Groups service.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer        | View access groups and members                                                                                                                             |
| Operator      | Not applicable                                                                                                                                             |
| Editor        | View, create, edit, and delete groups   \n  \n Add or remove users from groups                                                                             |
| Administrator | View, create, edit, and delete groups   \n  \n Add or remove users including other administators  \n  \n Assign access to a group   \n  \n Manage access for working with access groups   \n  \n Enable or disable public access to resources at the account level |
{: caption="Roles and example actions for the IAM access groups service" caption-side="top"}


### IAM Access Management service
{: #access-management}

You can give users access to manage access policies and custom roles.

| Roles         | Actions                         |
|---------------|---------------|
| Viewer        | View access policies and custom roles   |
| Operator      | View access policies and custom roles   |
| Editor        | View and edit custom roles   \n  \n View IAM insights, policies, and settings |
| Administrator | View, create, edit, and delete custom roles   \n  \n View and update IAM settings  \n  \n Assign access to a group   \n  \n View, create, edit, and delete access policies |
{: caption="Roles and example actions for the IAM Access Management service" caption-side="top"}

#### Role Management
{: #custom-roles-account-management}

You can give users access to create, update, and delete custom roles for services in the account.
Child service of the IAM Access Management service.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View custom roles         |
| Operator      | Not applicable         |
| Editor        | Edit and update custom roles in an account |
| Administrator | Create, edit, update, and delete custom roles in an account  |
{: caption="Roles and example actions for the Role Management service" caption-side="top"}


### IAM Identity service
{: #identity-service-account-management}

You can give users access to manage service IDs and identity providers (IdPs) by using the IAM Identity service. These actions apply to service IDs and IdPs within the account that the user didn't create. All users can create service IDs. They are the administrator for those IDs, and they can create the associated API key and access policies, but only users with the operator and administrator role can create IdPs. This account management service applies to the ability to view, update, delete, and assign access to service IDs in the account created by other users.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | View IDs              |
| Operator      | Create and delete IDs and API keys   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Delete trusted profiles         |
| Editor        | Create and update IDs and API keys   \n  \n View and update IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Update trusted profiles      |
| Administrator | Create, update, and delete IDs and API keys   \n  \n Assign access policies to IDs   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Create trusted profiles |
| User API Key Creator | Can create API keys when the account setting to restrict API key creation is enabled. |
| Service ID Creator | Can create service IDs when the account setting to restrict service ID creation is enabled. |
{: caption="Roles and example actions for the IAM Identity service" caption-side="top"}
{: #identity-service-acct-mgmt-ui}

### {{site.data.keyword.cloud-shell_notm}} settings
{: #shell-service-account-management}

You can assign users access to view and update {{site.data.keyword.cloud-shell_notm}} settings for the account. Only the account owner or a user with the {{site.data.keyword.cloud-shell_notm}} administrator role can view and update the settings.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | Not applicable        |
| Operator      | Not applicable        |
| Editor        | Not applicable        |
| Administrator | View and update {{site.data.keyword.cloud-shell_notm}} settings |
| Cloud Operator | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources. |
| Cloud Developer | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources and develop applications for {{site.data.keyword.cloud_notm}} (Web Preview enabled). |
| File Manager | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}}resources and manage files in your workspace (File Upload and File Download enabled). |
{: caption="Roles and example actions for the {{site.data.keyword.cloud-shell_notm}} service" caption-side="top"}

### License and entitlement
{: #license-entitlement-management}

You can assign users access to manage licenses and entitlements within an account. Any member of an account can view and use an account’s entitlement.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        |  Not applicable                                                                                            |
| Operator      |  Not applicable                                                                                            |
| Editor        |  Editors can create entitlements and view, update, bind, or delete only the entitlements they acquired.    |
| Administrator |  Administrators can create entitlements and view, update, bind, or delete any entitlements in the account. |
{: caption="Roles and example actions for the license and entitlement service" caption-side="top"}

### Platform analytics
{: #platform-analytics-account-management}

You can give users access to view, create, and share data charts.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View, search, create, update, and share data and charts |
| Administrator | View, search, create, update, and share data and charts. Assign access to Platform Analytics. |
{: caption="Roles and example actions for the Platform Analytics service" caption-side="top"}

### Partner Center
{: #pc-buildgrow-account-management}

You can give users access to view and edit partner profile details, offers, fast tracks, and to create and view support cases.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View details about partner profile, offers, fast tracks, support cases. |
| Editor        | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
| Operator      |  |
| Administrator | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
{: caption="Roles and example actions for the Partner Center service" caption-side="top"}

### Partner Center - Sell
{: #prod-lifecycle-account-management}

You can give users access to onboard, validate, and publish products.

| Roles         | Actions                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| Administrator | Create, edit, validate, and publish products |
| Editor        | Validate and edit products |
| Approver      | Approves or rejects a workflow instance's task |
{: caption="Roles and example actions for the Partner Center - Sell service" caption-side="top"}

### Projects
{: #projects-account-management}

You can give users access to configure, validate, and monitor Infrastructure as Code (IaC) deployments.

| Roles         | Actions                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| Viewer        | View details about projects, configurations, and deployments. |
| Operator | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration|
| Editor        | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources |
| Administrator     | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources. \n \n Force approve changes that failed validation |
{: caption="Roles and example actions for the {{site.data.keyword.cloud_notm}} Projects service" caption-side="top"}


### {{site.data.keyword.compliance_short}}
{: #security-compliance-account-management}

You can give users access to create, update, and delete resources for the {{site.data.keyword.compliance_short}} service in the account that you are assigned access.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------|
| Viewer        | View available profiles and attachments   \n  \n View created resources such as scopes, credentials, or rules   \n  \n View global settings for the service |
| Operator      | Access the {{site.data.keyword.compliance_short}} dashboard to view current posture and results   \n  \n Create an audit log for monitoring compliance activity |
| Editor        | Create, update, or delete objects such as scopes, credentials, and collectors   \n  \n Update the parameter settings of a goal   \n  \n Create, update, or delete rules and templates   \n  \n Edit global admin settings for the service |
| Administrator | Perform all platform actions based on the resource that this role is being assigned, including assigning access policies to other users. |
| Manager       | Permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
| Reader        | Perform read-only actions within a service such as viewing service-specific resources. |
| Writer        | Permissions beyond the reader role, including creating and editing service-specific resources. |
{: caption="Roles and example actions for the {{site.data.keyword.compliance_short}} service" caption-side="top"}


### Software instance
{: #sw-instance-account-management}

You can give users access to create, delete, or update a software instance. And, you can give users access to view the details page and the logs for the software instance.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View the software instance details page |
| Operator      | Update a software instance   \n  \n View the details page for the software instance |
| Editor        | Create, delete, update a software instance   \n  \n View the details page for the software instance |
| Administrator | Create, delete, update a software instance   \n  \n View the details page for the software instance   \n  \n View the logs for the software instance   \n  \n Assign IAM permissions |
{: caption="Roles and example actions for the Software instance service" caption-side="top"}

### Support center
{: #support-center-account-management}

You can give users access to manage support cases.

| Roles         | Actions                                                                       |
|---------------|-------------------------------------------------------------------------------|
| Viewer        |  View cases   \n  \n Search cases                                             |
| Operator      |  Not applicable                                                               |
| Editor        |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
| Administrator |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
{: caption="Roles and example actions for the Support Center service" caption-side="top"}

Assign users the viewer role on the user management service in addition to a support center access policy so the user can see all cases in the account regardless of user list visibility settings. If the user list visibility is set to be restricted, this can limit a user's ability to view, search, and manage support cases in an account that they didn't open themselves.
{: tip}

### User management
{: #user-management-account-management}

You can give users access to view users in an account, invite and remove users, and view and update user profile settings.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View users in the account   \n  \n View user profile settings                                          |
| Operator      | View users in the account   \n  \n View user profile settings                                          |
| Editor        | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
| Administrator | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
{: caption="Roles and example actions for the User Management service" caption-side="top"}

The viewer role on the user management service is a role that is commonly assigned for users assigned a role to view or manage support cases. If an account owner restricts the visibility of the user list in the IAM settings, users can't see support cases that are opened by other users in the account. However, if they are assigned the viewer role for the user management service, the user list visibility setting doesn't affect the ability to view cases in the account.
{: tip}

### {{site.data.keyword.atracker_short}}
{: #activty-tracker-account-management}

You can give users access to run platform actions.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Operator      | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Editor        | View, create, update, and delete {{site.data.keyword.atracker_short}} resources. |
| Administrator | View, create, update, and delete {{site.data.keyword.atracker_short}} resources.   \n  \n Assign access policies to manage {{site.data.keyword.atracker_short}} resources to other users in the account. |
{: caption="Roles and example actions for the {{site.data.keyword.atracker_short}} service" caption-side="top"}



## Account management service names
{: #account-management-servicenames}
{: api}

If you are assigning access by using the CLI or API, the account management services use the following attributes and values:

| Account management service         | Attribute and value   |
|---------------|---------------------------------|
| All Account Management services | `serviceType=platform_service` |
| All IAM Account Management services | `service_group_id=IAM` |
| Billing | `serviceName=billing` |
| Catalog management | `serviceName=globalcatalog-collection` |
| Context-based restrictions | `serviceName=context-based-restrictions`|
| Enterprise | `serviceName=enterprise` |
| Global catalog | `serviceName=globalcatalog` |
| IAM Access Groups service | `serviceName=iam-groups` |
| IAM Identity service | `serviceName=iam-identity` |
| {{site.data.keyword.cloud-shell_notm}} | `serviceName=cloudshell` |
| License and entitlement | `serviceName=entitlement` |
| Projects | `serviceName=project` |
| Role management | `serviceName=iam-access-management` |
| {{site.data.keyword.compliance_short}} | `serviceName=security-compliance` |
| Support center| `serviceName=support` |
| User management | `serviceName=user-management` |
{: caption="Account management service names" caption-side="top"}

## Assigning access by using the API
{: #api-acct-mgmt}
{: api}

The following example assigns a policy with the Administrator role on the IAM Access groups account management service.

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
          "value": "IBMid-123453user"
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
          "name": "serviceName",
          "value": "iam-groups"
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
        .value("EXAMPLE_USER_ID")
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

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
        .name("serviceName")
        .value("iam-groups")
        .operator("stringEquals")
        .build();

PolicyResource policyResources = new PolicyResource.Builder()
        .addAttributes(accountIdResourceAttribute)
        .addAttributes(serviceNameResourceAttribute)
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
        value: "exampleUserId",
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
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: 'iam-groups',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceNameResourceAttribute]
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
  attributes=[SubjectAttribute(name='iam_id', value='example_user_id')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:iam::::role:Administrator')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='iam-groups')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_name_resource_attribute])

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
  Value: core.StringPtr("exampleUserID"),
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
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("iam-groups"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute},
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

The following example assigns a policy with the Administrator role on **All Account Management services**.

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
          "value": "IBMid-123453user"
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
        .value("EXAMPLE_USER_ID")
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
        value: "exampleUserId",
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
  attributes=[SubjectAttribute(name='iam_id', value='example_user_id')])
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
  Value: core.StringPtr("exampleUserID"),
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

## Actions and roles for account management services
{: #account-management-actions-roles-api}
{: api}

The following tables outline the actions that users can take when they are assigned a specific role for each account management service. Review the information to ensure that you are assigning the correct level of access to your users.

### All Account Management services
{: #all-account-management-api}

To quickly give users a wide range of account management access, you can assign a policy on all account management services. When a user is assigned a role on **All Account Management services**, they can complete all of the actions that are associated with that role for each individual service.

The group of **All Account Management services** includes the following services:
- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role management
- User Management
- Billing
- Catalog management
- Context-based restrictions
- Enterprise
- Global catalog
- IBM Cloud shell settings
- License and entitlement
- Partner Center
- Partner Center - Sell
- Projects
- Security and Compliance Center
- Software instance
- Support center

| Roles         | Actions | role_ID value |
|---------------|---------|---------------|
| Viewer        | All viewer role actions for the account management services                                                  | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | All operator role actions for the account management services  | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | All editor role actions for the account management services and the ability to create resource groups        | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | All administrator role actions for the account management services and the ability to create resource groups | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for a policy on all account management services" caption-side="top"}

### All IAM Account Management services
{: #all-iam-api}

Identity and Access Management (IAM) services make up a subset of all account management services. Give users access to all IAM account management services so that they can work with the following services:

- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role Management
- User Management

| Roles         | Actions | role_ID value |
|---------------|---------|---------------|
| Viewer        | All viewer role actions for IAM services | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | All operator role actions for IAM services | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | All editor role actions for IAM services and the ability to create resource groups        |  `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | All administrator role actions for IAM services and the ability to create resource groups | `crn:v1:bluemix:public:iam::::role:Administrator` |
| User API key creator | Create API keys when the account setting to restrict API key creation is enabled | `crn:v1:bluemix:public:iam-identity::::serviceRole:UserApiKeyCreator` |
| Service ID creator | Create service IDs when the account setting to restrict service ID creation is enabled | `crn:v1:bluemix:public:iam-identity::::serviceRole:ServiceIdCreator` |
| Template Administrator | Create enterprise IAM templates for access groups, trusted profiles, account settings, and policies. This role is available in only the root enterprise account. | `crn:v1:bluemix:public:iam::::role:TemplateAdministrator` |
| Template Assignment Administrator | Assign enterprise IAM templates to child accounts. This role is available in only the root enterprise account. | `crn:v1:bluemix:public:iam::::role:TemplateAssignmentAdministrator` |
{: caption="Roles and example actions for a policy on all IAM account management services" caption-side="top"}

Some roles that you might assign on a policy for **All IAM Account Management services** affect only certain resources. For example, the role Service ID Creator is relevant to only the IAM Identity service.
{: note}

### Billing
{: #billing-acct-mgmt-api}

You can give users access to update account settings, view subscriptions, view offers, apply subscription and feature codes, update spending limits, and track usage by using the Billing service.

| Roles         | Actions                                                                                                    | role_ID value    |
|---------------|------------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View account feature settings   \n  \n View subscriptions in account   \n  \n View account name   \n  \n View subscription balances and track usage | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | View account feature settings   \n  \n View subscriptions in account   \n  \n View and change account name | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage   \n  \n Create an enterprise | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Billing service" caption-side="top"}

It's possible to view subscription balances and usage from the Account settings page, but you can't view the Account settings page with the Viewer or Operator roles. To access the Account settings page and your subscription information from that page, you need the Editor role or higher.
{: note}

### Catalog management
{: #catalog-management-account-management-api}

You can give users access to view private catalogs and catalog filters, create private catalogs, add software to private catalogs, and set catalog filters.

| Roles         | Actions                                                                                                | role_ID value    |
|---------------|--------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View account-level filters set for the {{site.data.keyword.cloud_notm}} catalog   \n  \n View private catalogs | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Set account-level filters for the {{site.data.keyword.cloud_notm}} catalog   \n  \n Create, update, and delete private catalogs   \n  \n Publish {{site.data.keyword.IBM_notm}}-approved products   \n  \n Assign access policies | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Publisher     | Publish products that are approved by {{site.data.keyword.IBM_notm}} from a private catalog | `crn:v1:bluemix:public:globalcatalog-collection::::serviceRole:Promoter`
{: caption="Roles and example actions for the catalog management service" caption-side="top"}

### Context-based restrictions
{: #cbr-account-management-api}

You can give users access to view, create, update, and remove network zones. To create a context-based restriction rule for a service, you must be assigned an IAM policy with the Administrator role the service you are creating a rule against. For example, if you want to create a rule to protect a **Key Protect** instance, you must be assigned the Administrator role on the **Key Protect** service and the Viewer role or higher on the **Context-based restrictions** service.

The Viewer role on the Context-based restrictions service allows you to add network zones to your rule.
{: note}

| Roles         | Actions                                                                                                | role_ID value    |
|---------------|--------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View network zones|                                  `crn:v1:bluemix:public:iam::::role:Viewer` |
| Editor        | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones  | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the context-based restrictions service" caption-side="top"}

You can give users access to view, create, update, and remove context-based restrictions and network zones.

### Enterprise
{: #enterprise-account-management-api}

You can use the Enterprise service to assign users access to manage an enterprise by creating accounts within the enterprise, assigning accounts to account groups, naming account groups, and more. This type of policy works only if it is assigned within the enterprise account.

| Roles               | Actions                                                                                                                                    | role_ID value    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Viewer              | View the enterprise, account groups, and accounts                                                                                          | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator            | Not applicable                                                                                          |  |
| Editor              | View and update the enterprise name and domain, create accounts and account groups, view usage reports, and import accounts. | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator       | View and update the enterprise name and domain, create accounts and account groups, move accounts between account groups, import existing accounts, and view usage reports | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Usage report viewer | View the enterprise, accounts, and account groups and view usage reports for all accounts in the enterprise.                               | `crn:v1:bluemix:public:enterprise::::serviceRole:UsageReportsViewer` |
{: caption="Roles and example actions for the Enterprise service" caption-side="top"}

### Global catalog
{: #global-catalog-account-management-api}

You can give users access to view private products in the catalog or change the visibility of private products for other users in the account.

| Roles         | Actions                                                                                                | role_ID value    |
|---------------|--------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View private services                                                                                  | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Not applicable                                                                                         | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | Change object metadata but can't change visibility for private services                                | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Change object metadata or visibility for private services, and restrict visibility of a public service | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Global Catalog service" caption-side="top"}

### IAM Access Groups
{: #access-groups-account-management-api}

You can give users access to view, create, edit, and delete access groups in the account by using the IAM Access Groups service.

| Roles         | Actions                                                                                                                                                    | role_ID value    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View access groups and members                                                                                                                             | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Not applicable                                                                                                                                             |  |
| Editor        | View, create, edit, and delete groups   \n  \n Add or remove users from groups                                                                             | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View, create, edit, and delete groups   \n  \n Add or remove users   \n  \n Assign access to a group   \n  \n Manage access for working with access groups   \n  \n Enable or disable public access to resources at the account level | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the IAM access groups service" caption-side="top"}

### IAM Access Management service
{: #access-management-api}

You can give users access to manage access policies and custom roles.

| Roles         | Actions       | role_ID value    |
|---------------|---------------|---------------|
| Viewer        | View access policies and custom roles   | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | View access policies and custom roles   | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View and edit custom roles   \n  \n View IAM insights, policies, and settings | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View, create, edit, and delete custom roles   \n  \n View and update IAM settings  \n  \n Assign access to a group   \n  \n View, create, edit, and delete access policies | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the IAM Access Management service" caption-side="top"}


#### Role Management
{: #custom-roles-account-management-api}

You can give users access to create, update, and delete custom roles for services in the account.

| Roles         | Actions                            | role_ID value    |
|---------------|------------------------------------|------------|
| Viewer        | View custom roles         | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Not applicable             | |
| Editor        | Edit and update custom roles in an account          | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Create, edit, update, and delete custom roles in an account  | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Access management service" caption-side="top"}

### IAM Identity service
{: #identity-service-account-management-api}

You can give users access to manage service IDs and identity providers (IdPs) by using the IAM Identity service. These actions apply to service IDs and IdPs within the account that the user didn't create. All users can create service IDs. They are the administrator for those IDs, and they can create the associated API key and access policies, but only users with the operator and administrator role can create IdPs. This account management service applies to the ability to view, update, delete, and assign access to service IDs in the account created by other users.

| Roles         | Actions                                                                                           | role_ID value    |
|---------------|---------------------------------------------------------------------------------------------------|------------|
| Viewer        | View IDs              | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Create and delete IDs and API keys   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Delete trusted profiles         | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | Create and update IDs and API keys   \n  \n View and update IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Update trusted profiles | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Create, update, and delete IDs and API keys   \n  \n Assign access policies to IDs   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Create trusted profiles | `crn:v1:bluemix:public:iam::::role:Administrator` |
| User API Key Creator | Can create API keys when the account setting to restrict API key creation is enabled. | `crn:v1:bluemix:public:iam-identity::::serviceRole:UserApiKeyCreator` |
| Service ID Creator | Can create service IDs when the account setting to restrict service ID creation is enabled. | `crn:v1:bluemix:public:iam-identity::::serviceRole:ServiceIdCreator` |
{: caption="Roles and example actions for the IAM Identity service" caption-side="top"}
{: #identity-service-acct-mgmt-api}

### {{site.data.keyword.cloud-shell_notm}} settings
{: #shell-service-account-management-api}

You can assign users access to view and update {{site.data.keyword.cloud-shell_notm}} settings for the account. Only the account owner or a user with the {{site.data.keyword.cloud-shell_notm}} administrator role can view and update the settings.

| Roles         | Actions                                                                                           | role_ID value    |
|---------------|---------------------------------------------------------------------------------------------------|------------|
| Viewer        | Not applicable        | |
| Operator      | Not applicable        | |
| Editor        | Not applicable        | |
| Administrator | View and update {{site.data.keyword.cloud-shell_notm}} settings | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Cloud Operator | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources. | `crn:v1:bluemix:public:cloudshell::::serviceRole:CloudOperator` |
| Cloud Developer | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources and develop applications for {{site.data.keyword.cloud_notm}} (Web Preview enabled). | `crn:v1:bluemix:public:cloudshell::::serviceRole:CloudDeveloper` |
| File Manager | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}}resources and manage files in your workspace (File Upload and File Download enabled). | `crn:v1:bluemix:public:cloudshell::::serviceRole:FileManager` |
{: caption="Roles and example actions for the {{site.data.keyword.cloud-shell_notm}} service" caption-side="top"}

### License and entitlement
{: #license-entitlement-management-api}

You can assign users access to manage licenses and entitlements within an account. Any member of an account can view and use an account’s entitlement.

| Roles         | Actions                                                                                                    | role_ID value    |
|---------------|------------------------------------------------------------------------------------------------------------|------------|
| Viewer        |  Not applicable                                                                                            |            |
| Operator      |  Not applicable                                                                                            |            |
| Editor        |  Editors can create entitlements and view, update, bind, or delete only the entitlements they acquired.    | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator |  Administrators can create entitlements and view, update, bind, or delete any entitlements in the account. | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the license and entitlement service" caption-side="top"}

### Platform analytics
{: #platform-analytics-account-management-api}

You can give users access to view, create, and share data charts.

| Roles         | Actions                                                 | role_ID value    |
|---------------|---------------------------------------------------------|------------|
| Viewer        | View, search, create, update, and share data and charts | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Administrator | View, search, create, update, and share data and charts. Assign access to Platform Analytics. |  `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Platform Analytics service" caption-side="top"}

### Partner Center
{: #pc-buildgrow-account-management-api}

You can give users access to view and edit partner profile details, offers, fast tracks, and to create and view support cases.

| Roles         | Actions                                                 | role_ID value    |
|---------------|---------------------------------------------------------|------------|
| Viewer        | View details about partner profile, offers, fast tracks, support cases. | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Editor        | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. | `crn:v1:bluemix:public:iam::::role:Editor` |
| Operator      |  |
| Administrator | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Partner Center service" caption-side="top"}

### Partner Center - Sell
{: #prod-lifecycle-account-management-api}

You can give users access to onboard, validate, and publish products.

| Roles         | Actions | role_ID value    |
|---------------|---------|------------------|
| Administrator | Create, edit, validate, and publish products | | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Editor        | Validate and edit products | `crn:v1:bluemix:public:iam::::role:Editor` |
| Approver      | Approves or rejects a workflow instance's task | `crn:v1:bluemix:public:product-lifecycle::::serviceRole:LifecycleApprover` |
{: caption="Roles and example actions for the Partner Center - Sell service" caption-side="top"}

### Projects
{: #projects-account-management-api}

You can give users access to configure, validate, and monitor Infrastructure as Code (IaC) deployments.

| Roles         | Actions | role_ID value    |
|---------------|---------|-----------------|
| Viewer        | View details about projects, configurations, and deployments. | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration| `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources |  `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator     | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources. \n \n Force approve changes that failed validation | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the {{site.data.keyword.cloud_notm}} Projects service" caption-side="top"}

### {{site.data.keyword.compliance_short}}
{: #security-compliance-account-management-api}

You can give users access to create, update, and delete resources for the {{site.data.keyword.compliance_short}} service in the account that you are assigned access.

| Roles         | Actions                                                                                                                   | role_ID value    |
|---------------|---------------------------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View available profiles and attachments   \n  \n View created resources such as scopes, credentials, or rules   \n  \n View global settings for the service | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Access the {{site.data.keyword.compliance_short}} dashboard to view current posture and results \n \n Create an audit log for monitoring compliance activity | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | Create, update, or delete objects such as scopes, credentials, and collectors   \n  \n Update the parameter settings of a goal   \n  \n Create, update, or delete rules and templates   \n  \n Edit global admin settings for the service | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Perform all platform actions based on the resource that this role is being assigned, including assigning access policies to other users. | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Manager       | Permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |`crn:v1:bluemix:public:iam::::serviceRole:Manager` |
| Reader        | Perform read-only actions within a service such as viewing service-specific resources. | `crn:v1:bluemix:public:iam::::serviceRole:Reader` |
| Writer        | Permissions beyond the reader role, including creating and editing service-specific resources. | `crn:v1:bluemix:public:iam::::serviceRole:Writer` |
{: caption="Roles and example actions for the {{site.data.keyword.compliance_short}} service" caption-side="top"}


### Software instance
{: #sw-instance-account-management-api}

You can give users access to create, delete, or update a software instance. And, you can give users access to view the details page and the logs for the software instance.

| Roles         | Actions                            | role_ID value    |
|---------------|------------------------------------|------------|
| Viewer        | View the software instance details page | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | Update a software instance   \n  \n View the details page for the software instance | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | Create, delete, update a software instance   \n  \n View the details page for the software instance | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | Create, delete, update a software instance   \n  \n View the details page for the software instance   \n  \n View the logs for the software instance   \n  \n Assign IAM permissions | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Software instance service" caption-side="top"}

### Support center
{: #support-center-account-management-api}

You can give users access to manage support cases.

| Roles         | Actions                                                                       | role_ID value    |
|---------------|-------------------------------------------------------------------------------|------------|
| Viewer        |  View cases   \n  \n Search cases                                             | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      |  Not applicable                                                               | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the Support Center service" caption-side="top"}

Assign users the viewer role on the user management service in addition to a support center access policy so the user can see all cases in the account regardless of user list visibility settings. If the user list visibility is set to be restricted, a user's ability to view, search, and manage support cases in an account that they didn't open themselves can be limited.
{: tip}

### User management
{: #user-management-account-management-api}

You can give users access to view users in an account, invite and remove users, and view and update user profile settings.

| Roles         | Actions                                                                                                | role_ID value    |
|---------------|--------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View users in the account   \n  \n View user profile settings                                          | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | View users in the account   \n  \n View user profile settings                                          | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View, invite, remove, and update users from the account   \n  \n View and update user profile settings | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View, invite, remove, and update users from the account   \n  \n View and update user profile settings | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the User Management service" caption-side="top"}

The viewer role on the user management service is a role that is commonly assigned for users assigned a role to view or manage support cases. If an account owner restricts the visibility of the user list in the IAM settings, users can't see support cases that are opened by other users in the account. However, if they are assigned the viewer role for the user management service, the user list visibility setting doesn't affect the ability to view cases in the account.
{: tip}

### {{site.data.keyword.atracker_short}}
{: #activty-tracker-account-management-api}

You can give users access to run platform actions.

| Roles         | Actions                                                                                                | role_ID value    |
|---------------|--------------------------------------------------------------------------------------------------------|------------|
| Viewer        | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator      | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View, create, update, and delete {{site.data.keyword.atracker_short}} resources. | `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator | View, create, update, and delete {{site.data.keyword.atracker_short}} resources.   \n  \n Assign access policies to manage {{site.data.keyword.atracker_short}} resources to other users in the account. | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the {{site.data.keyword.atracker_short}} service" caption-side="top"}



## Account management service names
{: #account-management-servicenames-cli}
{: cli}

If you are assigning access by using the CLI or API, the account management services use the following attributes and values:

| Account management service         | Attribute and value   |
|---------------|---------------------------------|
| All Account Management services | `serviceType=platform_service` |
| All IAM Account Management services | `service_group_id=IAM` |
| Billing | `serviceName=billing` |
| Catalog management | `serviceName=globalcatalog-collection` |
| Context-based restrictions | `serviceName=context-based-restrictions`|
| Enterprise | `serviceName=enterprise` |
| Global catalog | `serviceName=globalcatalog` |
| IAM Access Groups service | `serviceName=iam-groups` |
| IAM Identity service | `serviceName=iam-identity` |
| {{site.data.keyword.cloud-shell_notm}} | `serviceName=cloudshell` |
| License and entitlement | `serviceName=entitlement` |
| Projects | `serviceName=project` |
| Role management | `serviceName=iam-access-management` |
| {{site.data.keyword.compliance_short}} | `serviceName=security-compliance` |
| Support center| `serviceName=support` |
| User management | `serviceName=user-management` |
{: caption="Account management service names" caption-side="top"}

## Assigning access by using the CLI
{: #cli-acct-mgmt}
{: cli}

To assign access, run the `user-policy-create` command. For more information, see [ibmcloud iam user-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create). The following example command assigns a policy with the User API key creator role for the IAM Identity account management service.

```sh
ibmcloud iam user-policy-create name@example.com --roles "User API key creator" --service-name iam-identity
```
{: pre}

For service names to use in the CLI command for each account management service, see Table 1. However, for a policy on all account management services in the CLI, use `--account-management` instead of `--service-name SERVICE_NAME`. For roles that are more than one word, use the display name with quotations.
{: tip}

The following example command assigns a policy with the Administrator role for All Account Management services.

```sh
ibmcloud iam user-policy-create name.example.com --roles Administrator --attributes serviceType=service
```
{: pre}

## Actions and roles for account management services
{: #account-management-actions-roles-cli}
{: cli}

The following tables outline the actions that users can take when they are assigned a specific role for each account management service. Review the information to ensure that you are assigning the correct level of access to your users.

### All Account Management services
{: #all-account-management-cli}

To quickly give users a wide-ranging set of account management access, you can assign a policy on all account management services. When a user is assigned a role on **All Account Management services**, they can complete all of the actions that are associated with that role for each individual service.

The group of **All Account Management services** includes the following services:
- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role management
- User Management
- Billing
- Catalog management
- Context-based restrictions
- Enterprise
- Global catalog
- IBM Cloud shell settings
- License and entitlement
- Partner Center
- Partner Center - Sell
- Projects
- Security and Compliance Center
- Software instance
- Support center

| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for the account management services                                                  |
| Operator      | All operator role actions for the account management services                                                |
| Editor        | All editor role actions for the account management services and the ability to create resource groups        |
| Administrator | All administrator role actions for the account management services and the ability to create resource groups |
{: caption="Roles and example actions for a policy on all account management services" caption-side="top"}

### All IAM Account Management services
{: #all-iam-cli}

Identity and Access Management (IAM) services make up a subset of all account management services. Give users access to all IAM account management services so that they can work with the following services:

- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role Management
- User Management

| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for IAM services                                                  |
| Operator      | All operator role actions for IAM services                                                |
| Editor        | All editor role actions for IAM services and the ability to create resource groups        |
| Administrator | All administrator role actions for IAM services and the ability to create resource groups |
| User API key creator | Create API keys when the account setting to restrict API key creation is enabled |
| Service ID creator | Create service IDs when the account setting to restrict service ID creation is enabled |
| Template Administrator | Create enterprise IAM templates for access groups, trusted profiles, account settings, and policies. This role is available in only the root enterprise account. |
| Template Assignment Administrator | Assign enterprise IAM templates to child accounts. This role is available in only the root enterprise account. |
{: caption="Roles and example actions for a policy on all IAM account management services" caption-side="top"}

Some roles that you might assign on a policy for **All IAM Account Management services** affect only certain resources. For example, the role Service ID Creator is relevant to only the IAM Identity service.
{: note}

### Billing
{: #billing-acct-mgmt-cli}

You can give users access to update account settings, view subscriptions, view offers, apply subscription and feature codes, update spending limits, and track usage by using the Billing service.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        | View account feature settings   \n  \n View subscriptions in account   \n  \n View account name   \n  \n View subscription balances and track usage           |
| Operator      | View account feature settings   \n  \n View subscriptions in account   \n  \n View and change account name |
| Editor        | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage |
| Administrator | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage   \n  \n Create an enterprise |
{: caption="Roles and example actions for the Billing service" caption-side="top"}

It's possible to view subscription balances and usage from the Account settings page, but you can't view the Account settings page with the Viewer or Operator roles. To access the Account settings page and your subscription information from that page, you need the Editor role or higher.
{: note}

### Catalog management
{: #catalog-management-account-management-cli}

You can give users access to view private catalogs and catalog filters, create private catalogs, add software to private catalogs, and set catalog filters.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View account-level filters set for the {{site.data.keyword.cloud_notm}} catalog   \n  \n View private catalogs                                          |
| Operator      | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters    |
| Editor        | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters |
| Administrator | Set account-level filters for the {{site.data.keyword.cloud_notm}} catalog   \n  \n Create, update, and delete private catalogs   \n  \n Publish {{site.data.keyword.IBM_notm}}-approved products   \n  \n Assign access policies |
| Publisher     | Publish products that are approved by {{site.data.keyword.IBM_notm}} from a private catalog |
{: caption="Roles and example actions for the catalog management service" caption-side="top"}

### Context-based restrictions
{: #cbr-account-management-cli}

You can give users access to view, create, update, and remove network zones. To create a context-based restriction rule for a service, you must be assigned an IAM policy with the Administrator role the service you are creating a rule against. For example, if you want to create a rule to protect a **Key Protect** instance, you must be assigned the Administrator role on the **Key Protect** service and the Viewer role or higher on the  **Context-based restrictions** service.

The Viewer role on the Context-based restrictions service allows you to add network zones to your rule.
{: note}

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View network zones|
| Editor        | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones  |
| Administrator | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones |
{: caption="Roles and example actions for the context-based restrictions service" caption-side="top"}


### Enterprise
{: #enterprise-account-management-cli}

You can use the Enterprise service to assign users access to manage an enterprise by creating accounts within the enterprise, assigning accounts to account groups, naming account groups, and more. This type of policy works only if it is assigned within the enterprise account.

| Roles               | Actions                                                                                                                                    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer              | View the enterprise, account groups, and accounts                                                                                          |
| Operator            | Not applicable                                                                                          |
| Editor              | View and update the enterprise name and domain, create accounts and account groups, view usage reports, and import accounts. |
| Administrator       | View and update the enterprise name and domain, create accounts and account groups, move accounts between account groups, import existing accounts, and view usage reports |
| Usage report viewer | View the enterprise, accounts, and account groups and view usage reports for all accounts in the enterprise.                               |
{: caption="Roles and example actions for the Enterprise service" caption-side="top"}

### Global catalog
{: #global-catalog-account-management-cli}

You can give users access to view private products in the catalog or change the visibility of private products for other users in the account.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View private services                                                                                  |
| Operator      | Not applicable                                                                                         |
| Editor        | Change object metadata but can't change visibility for private services                                |
| Administrator | Change object metadata or visibility for private services, and restrict visibility of a public service |
{: caption="Roles and example actions for the Global Catalog service" caption-side="top"}

### IAM Access Groups
{: #access-groups-account-management-cli}

You can give users access to view, create, edit, and delete access groups in the account by using the IAM Access Groups service.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer        | View access groups and members                                                                                                                             |
| Operator      | Not applicable                                                                                                                                             |
| Editor        | View, create, edit, and delete groups   \n  \n Add or remove users from groups                                                                             |
| Administrator | View, create, edit, and delete groups   \n  \n Add or remove users   \n  \n Assign access to a group   \n  \n Manage access for working with access groups   \n  \n Enable or disable public access to resources at the account level |
{: caption="Roles and example actions for the IAM access groups service" caption-side="top"}

### IAM Access Management service
{: #access-management-cli}

You can give users access to manage access policies and custom roles.

| Roles         | Actions                         |
|---------------|---------------|
| Viewer        | View access policies and custom roles   |
| Operator      | View access policies and custom roles   |
| Editor        | View and edit custom roles   \n  \n View IAM insights, policies, and settings |
| Administrator | View, create, edit, and delete custom roles   \n  \n View and update IAM settings  \n  \n Assign access to a group   \n  \n View, create, edit, and delete access policies |
{: caption="Roles and example actions for the IAM Access Management service" caption-side="top"}


#### Role Management
{: #custom-roles-account-management-cli}

You can give users access to create, update, and delete custom roles for services in the account.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View custom roles         |
| Operator      | Not applicable             |
| Editor        | Edit and update custom roles in an account          |
| Administrator | Create, edit, update, and delete custom roles in an account  |
{: caption="Roles and example actions for the Access management service" caption-side="top"}

### IAM Identity service
{: #identity-service-account-management-cli}

You can give users access to manage service IDs and identity providers (IdPs) by using the IAM Identity service. These actions apply to service IDs and IdPs within the account that the user didn't create. All users can create service IDs. They are the administrator for those IDs, and they can create the associated API key and access policies, but only users with the operator and administrator role can create IdPs. This account management service applies to the ability to view, update, delete, and assign access to service IDs in the account created by other users.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | View IDs              |
| Operator      | Create and delete IDs and API keys   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Delete trusted profiles         |
| Editor        | Create and update IDs and API keys   \n  \n View and update IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Update trusted profiles      |
| Administrator | Create, update, and delete IDs and API keys   \n  \n Assign access policies to IDs   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Create trusted profiles |
| User API Key Creator | Can create API keys when the account setting to restrict API key creation is enabled. |
| Service ID Creator | Can create service IDs when the account setting to restrict service ID creation is enabled. |
{: caption="Roles and example actions for the IAM Identity service" caption-side="top"}
{: #identity-service-acct-mgmt-cli}

### {{site.data.keyword.cloud-shell_notm}} settings
{: #shell-service-account-management-cli}

You can assign users access to view and update {{site.data.keyword.cloud-shell_notm}} settings for the account. Only the account owner or a user with the {{site.data.keyword.cloud-shell_notm}} administrator role can view and update the settings.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | Not applicable        |
| Operator      | Not applicable        |
| Editor        | Not applicable        |
| Administrator | View and update {{site.data.keyword.cloud-shell_notm}} settings |
| Cloud Operator | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources. |
| Cloud Developer | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources and develop applications for {{site.data.keyword.cloud_notm}} (Web Preview enabled). |
| File Manager | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}}resources and manage files in your workspace (File Upload and File Download enabled). |
{: caption="Roles and example actions for the {{site.data.keyword.cloud-shell_notm}} service" caption-side="top"}

### License and entitlement
{: #license-entitlement-management-cli}

You can assign users access to manage licenses and entitlements within an account. Any member of an account can view and use an account’s entitlement.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        |  Not applicable                                                                                            |
| Operator      |  Not applicable                                                                                            |
| Editor        |  Editors can create entitlements and view, update, bind, or delete only the entitlements they acquired.    |
| Administrator |  Administrators can create entitlements and view, update, bind, or delete any entitlements in the account. |
{: caption="Roles and example actions for the license and entitlement service" caption-side="top"}

### Platform analytics
{: #platform-analytics-account-management-cli}

You can give users access to view, create, and share data charts.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View, search, create, update, and share data and charts |
| Administrator | View, search, create, update, and share data and charts. Assign access to Platform Analytics. |
{: caption="Roles and example actions for the Platform Analytics service" caption-side="top"}

### Partner Center
{: #pc-buildgrow-account-management-cli}

You can give users access to view and edit partner profile details, offers, fast tracks, and to create and view support cases.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View details about partner profile, offers, fast tracks, support cases. |
| Editor        | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
| Operator      |  |
| Administrator | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
{: caption="Roles and example actions for the Partner Center service" caption-side="top"}

### Partner Center - Sell
{: #prod-lifecycle-account-management-cli}

You can give users access to onboard, validate, and publish products.

| Roles         | Actions                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| Administrator | Create, edit, validate, and publish products |
| Editor        | Validate and edit products |
| Approver      | Approves or rejects a workflow instance's task |
{: caption="Roles and example actions for the Partner Center - Sell service" caption-side="top"}

### Projects
{: #projects-account-management-cli}

You can give users access to configure, validate, and monitor Infrastructure as Code (IaC) deployments.

| Roles         | Actions | role_ID value    |
|---------------|---------|-----------------|
| Viewer        | View details about projects, configurations, and deployments. | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Operator | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration| `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor        | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources |  `crn:v1:bluemix:public:iam::::role:Editor` |
| Administrator     | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources. \n \n Force approve changes that failed validation | `crn:v1:bluemix:public:iam::::role:Administrator` |
{: caption="Roles and example actions for the {{site.data.keyword.cloud_notm}} Projects service" caption-side="top"}


### {{site.data.keyword.compliance_short}}
{: #security-compliance-account-management-cli}

You can give users access to create, update, and delete resources for the {{site.data.keyword.compliance_short}} service in the account that you are assigned access.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------|
| Viewer        | View available profiles and attachments   \n  \n View created resources such as scopes, credentials, or rules   \n  \n View global settings for the service |
| Operator      | Access the {{site.data.keyword.compliance_short}} dashboard to view current posture and results   \n  \n Create an audit log for monitoring compliance activity |
| Editor        | Create, update, or delete objects such as scopes, credentials, and collectors   \n  \n Update the parameter settings of a goal   \n  \n Create, update, or delete rules and templates   \n  \n Edit global admin settings for the service |
| Administrator | Perform all platform actions based on the resource that this role is being assigned, including assigning access policies to other users. |
| Manager       | Permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
| Reader        | Perform read-only actions within a service such as viewing service-specific resources. |
| Writer        | Permissions beyond the reader role, including creating and editing service-specific resources. |
{: caption="Roles and example actions for the {{site.data.keyword.compliance_short}} service" caption-side="top"}


### Software instance
{: #sw-instance-account-management-cli}

You can give users access to create, delete, or update a software instance. And, you can give users access to view the details page and the logs for the software instance.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View the software instance details page |
| Operator      | Update a software instance   \n  \n View the details page for the software instance |
| Editor        | Create, delete, update a software instance   \n  \n View the details page for the software instance |
| Administrator | Create, delete, update a software instance   \n  \n View the details page for the software instance   \n  \n View the logs for the software instance   \n  \n Assign IAM permissions |
{: caption="Roles and example actions for the Software instance service" caption-side="top"}

### Support center
{: #support-center-account-management-cli}

You can give users access to manage support cases.

| Roles         | Actions                                                                       |
|---------------|-------------------------------------------------------------------------------|
| Viewer        |  View cases   \n  \n Search cases                                             |
| Operator      |  Not applicable                                                               |
| Editor        |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
| Administrator |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
{: caption="Roles and example actions for the Support Center service" caption-side="top"}

Assign users the viewer role on the user management service in addition to a support center access policy so the user can see all cases in the account regardless of user list visibility settings. If the user list visibility is set to be restricted, this can limit a user's ability to view, search, and manage support cases in an account that they didn't open themselves.
{: tip}

### User management
{: #user-management-account-management-cli}

You can give users access to view users in an account, invite and remove users, and view and update user profile settings.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View users in the account   \n  \n View user profile settings                                          |
| Operator      | View users in the account   \n  \n View user profile settings                                          |
| Editor        | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
| Administrator | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
{: caption="Roles and example actions for the User Management service" caption-side="top"}

The viewer role on the user management service is a role that is commonly assigned for users assigned a role to view or manage support cases. If an account owner restricts the visibility of the user list in the IAM settings, users can't see support cases that are opened by other users in the account. However, if they are assigned the viewer role for the user management service, the user list visibility setting doesn't affect the ability to view cases in the account.
{: tip}

### {{site.data.keyword.atracker_short}}
{: #activty-tracker-account-management-cli}

You can give users access to run platform actions.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Operator      | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Editor        | View, create, update, and delete {{site.data.keyword.atracker_short}} resources. |
| Administrator | View, create, update, and delete {{site.data.keyword.atracker_short}} resources.   \n  \n Assign access policies to manage {{site.data.keyword.atracker_short}} resources to other users in the account. |
{: caption="Roles and example actions for the {{site.data.keyword.atracker_short}} service" caption-side="top"}




## Assigning access by using Terraform
{: #terraform-acct-mgmt}
{: terraform}

Before you can assign access by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to assign access by using Terraform:

1. Create an argument in your `main.tf` file. The following example assigns a policy with the `Viewer` role on the IAM Access groups account management service.

   ```terraform
   resource "ibm_iam_access_group" "accgrp" {
    name = "test"
   }

   resource "ibm_iam_access_group_policy" "policy" {
    access_group_id = ibm_iam_access_group.accgrp.id
    roles           = ["Viewer"]
   }
   ```
   {: codeblock}

   You can specify the ID of the access group on the `access_group_id` option. For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group_policy){: external} page.

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

## Actions and roles for account management services
{: #account-management-actions-roles-terra}
{: terraform}

The following tables outline the actions that users can take when they are assigned a specific role for each account management service. Review the information to ensure that you are assigning the correct level of access to your users.

### All Account Management services
{: #all-account-management-terra}

To quickly give users a wide-ranging set of account management access, you can assign a policy on all account management services. When a user is assigned a role on **All Account Management services**, they can complete all of the actions that are associated with that role for each individual service.

The group of **All Account Management services** includes the following services:
- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role management
- User Management
- Billing
- Catalog management
- Context-based restrictions
- Enterprise
- Global catalog
- IBM Cloud shell settings
- License and entitlement
- Partner Center
- Partner Center - Sell
- Projects
- Security and Compliance Center
- Software instance
- Support center

| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for the account management services                                                  |
| Operator      | All operator role actions for the account management services                                                |
| Editor        | All editor role actions for the account management services and the ability to create resource groups        |
| Administrator | All administrator role actions for the account management services and the ability to create resource groups |
{: caption="Roles and example actions for a policy on account management services" caption-side="top"}

### All IAM Account Management services
{: #all-iam-terra}

Identity and Access Management (IAM) services make up a subset of all account management services. Give users access to all IAM account management services so that they can work with the following services:

- IAM Access Groups
- IAM Identity service
- IAM Access Management
   - Role Management
- User Management

| Roles         | Actions                                                                                                      |
|---------------|--------------------------------------------------------------------------------------------------------------|
| Viewer        | All viewer role actions for IAM services                                                  |
| Operator      | All operator role actions for IAM services                                                |
| Editor        | All editor role actions for IAM services and the ability to create resource groups        |
| Administrator | All administrator role actions for IAM services and the ability to create resource groups |
| User API key creator | Create API keys when the account setting to restrict API key creation is enabled |
| Service ID creator | Create service IDs when the account setting to restrict service ID creation is enabled |
| Template Administrator | Create enterprise IAM templates for access groups, trusted profiles, account settings, and policies. This role is available in only the root enterprise account. |
| Template Assignment Administrator | Assign enterprise IAM templates to child accounts. This role is available in only the root enterprise account. |
{: caption="Roles and example actions for a policy on all IAM account management services" caption-side="top"}

Some roles that you might assign on a policy for **All IAM Account Management services** affect only certain resources. For example, the role Service ID Creator is relevant to only the IAM Identity service.
{: note}

### Billing
{: #billing-acct-mgmt-terra}

You can give users access to update account settings, view subscriptions, view offers, apply subscription and feature codes, update spending limits, and track usage by using the Billing service.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        | View account feature settings   \n  \n View subscriptions in account   \n  \n View account name   \n  \n View subscription balances and track usage           |
| Operator      | View account feature settings   \n  \n View subscriptions in account   \n  \n View and change account name |
| Editor        | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage |
| Administrator | View and update account feature settings   \n  \n View subscriptions in account   \n  \n View offers in account   \n  \n View and apply subscription and feature codes   \n  \n View and change account name   \n  \n View and update spending limits   \n  \n Set spending notifications   \n  \n View subscription balances and track usage   \n  \n Create an enterprise |
{: caption="Roles and example actions for the Billing service" caption-side="top"}

It's possible to view subscription balances and usage from the Account settings page, but you can't view the Account settings page with the Viewer or Operator roles. To access the Account settings page and your subscription information from that page, you need the Editor role or higher.
{: note}

### Catalog management
{: #catalog-management-account-management-terra}

You can give users access to view private catalogs and catalog filters, create private catalogs, add software to private catalogs, and set catalog filters.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View account-level filters set for the {{site.data.keyword.cloud_notm}} catalog   \n  \n View private catalogs                                          |
| Operator      | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters    |
| Editor        | Create private catalogs   \n  \n Set filters for private catalogs   \n  \n Add and update software   \n  \n View account-level filters |
| Administrator | Set account-level filters for the {{site.data.keyword.cloud_notm}} catalog   \n  \n Create, update, and delete private catalogs   \n  \n Publish {{site.data.keyword.IBM_notm}}-approved products   \n  \n Assign access policies |
| Publisher     | Publish products that are approved by {{site.data.keyword.IBM_notm}} from a private catalog |
{: caption="Roles and example actions for the catalog management service" caption-side="top"}

### Context-based restrictions
{: #cbr-account-management-terra}

You can give users access to view, create, update, and remove network zones. To create a context-based restriction rule for a service, you must be assigned an IAM policy with the Administrator role the service you are creating a rule against. For example, if you want to create a rule to protect a **Key Protect** instance, you must be assigned the Administrator role on the **Key Protect** service and the Viewer role or higher on the  **Context-based restrictions** service.

The Viewer role on the Context-based restrictions service allows you to add network zones to your rule.
{: note}

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View network zones|
| Editor        | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones  |
| Administrator | View network zones   \n  \n Create network zones   \n  \n Update network zones   \n  \n Remove network zones |
{: caption="Roles and example actions for the context-based restrictions service" caption-side="top"}


### Enterprise
{: #enterprise-account-management-terra}

You can use the Enterprise service to assign users access to manage an enterprise by creating accounts within the enterprise, assigning accounts to account groups, naming account groups, and more. This type of policy works only if it is assigned within the enterprise account.

| Roles               | Actions                                                                                                                                    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer              | View the enterprise, account groups, and accounts                                                                                          |
| Operator            | Not applicable                                                                                          |
| Editor              | View and update the enterprise name and domain, create accounts and account groups, view usage reports, and import accounts. |
| Administrator       | View and update the enterprise name and domain, create accounts and account groups, move accounts between account groups, import existing accounts, and view usage reports |
| Usage report viewer | View the enterprise, accounts, and account groups and view usage reports for all accounts in the enterprise.                               |
{: caption="Roles and example actions for the Enterprise service" caption-side="top"}

### Global catalog
{: #global-catalog-account-management-terra}

You can give users access to view private products in the catalog or change the visibility of private products for other users in the account.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View private services                                                                                  |
| Operator      | Not applicable                                                                                         |
| Editor        | Change object metadata but can't change visibility for private services                                |
| Administrator | Change object metadata or visibility for private services, and restrict visibility of a public service |
{: caption="Roles and example actions for the Global Catalog service" caption-side="top"}

### IAM Access Groups
{: #access-groups-account-management-terra}

You can give users access to view, create, edit, and delete access groups in the account by using the IAM Access Groups service.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Viewer        | View access groups and members                                                                                                                             |
| Operator      | Not applicable                                                                                                                                             |
| Editor        | View, create, edit, and delete groups   \n  \n Add or remove users from groups                                                                             |
| Administrator | View, create, edit, and delete groups   \n  \n Add or remove users   \n  \n Assign access to a group   \n  \n Manage access for working with access groups   \n  \n Enable or disable public access to resources at the account level |
{: caption="Roles and example actions for the IAM access groups service" caption-side="top"}

### IAM Access Management service
{: #access-management-terra}

You can give users access to manage access policies and custom roles.

| Roles         | Actions                         |
|---------------|---------------|
| Viewer        | View access policies and custom roles   |
| Operator      | View access policies and custom roles   |
| Editor        | View and edit custom roles   \n  \n View IAM insights, policies, and settings |
| Administrator | View, create, edit, and delete custom roles   \n  \n View and update IAM settings  \n  \n Assign access to a group   \n  \n View, create, edit, and delete access policies |
{: caption="Roles and example actions for the IAM Access Management service" caption-side="top"}


#### Role Management
{: #custom-roles-account-management-terra}

You can give users access to create, update, and delete custom roles for services in the account.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View custom roles         |
| Operator      | Not applicable             |
| Editor        | Edit and update custom roles in an account          |
| Administrator | Create, edit, update, and delete custom roles in an account  |
{: caption="Roles and example actions for the Access management service" caption-side="top"}

### IAM Identity service
{: #identity-service-account-management-terra}

You can give users access to manage service IDs and identity providers (IdPs) by using the IAM Identity service. These actions apply to service IDs and IdPs within the account that the user didn't create. All users can create service IDs. They are the administrator for those IDs, and they can create the associated API key and access policies, but only users with the operator and administrator role can create IdPs. This account management service applies to the ability to view, update, delete, and assign access to service IDs in the account created by other users.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | View IDs              |
| Operator      | Create and delete IDs and API keys   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Delete trusted profiles         |
| Editor        | Create and update IDs and API keys   \n  \n View and update IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Update trusted profiles      |
| Administrator | Create, update, and delete IDs and API keys   \n  \n Assign access policies to IDs   \n  \n View, create, update, and delete IdPs   \n  \n Update IAM account setting for service IDs and user API key creation   \n  \n Create trusted profiles |
| User API Key Creator | Can create API keys when the account setting to restrict API key creation is enabled. |
| Service ID Creator | Can create service IDs when the account setting to restrict service ID creation is enabled. |
{: caption="Roles and example actions for the IAM Identity service" caption-side="top"}
{: #identity-service-acct-mgmt-terra}

### {{site.data.keyword.cloud-shell_notm}} settings
{: #shell-service-account-management-terra}

You can assign users access to view and update {{site.data.keyword.cloud-shell_notm}} settings for the account. Only the account owner or a user with the {{site.data.keyword.cloud-shell_notm}} administrator role can view and update the settings.

| Roles         | Actions                                                                                           |
|---------------|----------------------------------------------------------------------------------------------------|
| Viewer        | Not applicable        |
| Operator      | Not applicable        |
| Editor        | Not applicable        |
| Administrator | View and update {{site.data.keyword.cloud-shell_notm}} settings |
| Cloud Operator | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources. |
| Cloud Developer | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}} resources and develop applications for {{site.data.keyword.cloud_notm}} (Web Preview enabled). |
| File Manager | Create {{site.data.keyword.cloud-shell_short}} environments to manage {{site.data.keyword.cloud_notm}}resources and manage files in your workspace (File Upload and File Download enabled). |
{: caption="Roles and example actions for the {{site.data.keyword.cloud-shell_notm}} service" caption-side="top"}

### License and entitlement
{: #license-entitlement-management-terra}

You can assign users access to manage licenses and entitlements within an account. Any member of an account can view and use an account’s entitlement.

| Roles         | Actions                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------|
| Viewer        |  Not applicable                                                                                            |
| Operator      |  Not applicable                                                                                            |
| Editor        |  Editors can create entitlements and view, update, bind, or delete only the entitlements they acquired.    |
| Administrator |  Administrators can create entitlements and view, update, bind, or delete any entitlements in the account. |
{: caption="Roles and example actions for the license and entitlement service" caption-side="top"}

### Platform analytics
{: #platform-analytics-account-management-terra}

You can give users access to view, create, and share data charts.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View, search, create, update, and share data and charts |
| Administrator | View, search, create, update, and share data and charts. Assign access to Platform Analytics. |
{: caption="Roles and example actions for the Platform Analytics service" caption-side="top"}

### Partner Center
{: #pc-buildgrow-account-management-terra}

You can give users access to view and edit partner profile details, offers, fast tracks, and to create and view support cases.

| Roles         | Actions                                                 |
|---------------|---------------------------------------------------------|
| Viewer        | View details about partner profile, offers, fast tracks, support cases. |
| Editor        | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
| Operator      |  |
| Administrator | View and edit partner profile, offers, and fast tracks. Create, edit, and view support cases. |
{: caption="Roles and example actions for the Partner Center service" caption-side="top"}

### Partner Center - Sell
{: #prod-lifecycle-account-management-terra}

You can give users access to onboard, validate, and publish products.

| Roles         | Actions                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| Administrator | Create, edit, validate, and publish products |
| Editor        | Validate and edit products |
| Approver      | Approves or rejects a workflow instance's task |
{: caption="Roles and example actions for the Partner Center - Sell service" caption-side="top"}

### Projects
{: #projects-account-management-terra}

You can give users access to configure, validate, and monitor Infrastructure as Code (IaC) deployments.

| Roles         | Actions |
|---------------|---------|
| Viewer        | View details about projects, configurations, and deployments. |
| Operator | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration|
| Editor        | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources |
| Administrator     | View details about projects, configurations, and deployments \n \n Validate a configuration \n \n Edit a configuration \n \n Create a project \n \n Edit a project \n \n Delete a project \n \n Create a configuration \n \n  Discard a draft configuration \n \n Deploy configuration changes \n \n Destroy resources. \n \n Force approve changes that failed validation |
{: caption="Roles and example actions for the {{site.data.keyword.cloud_notm}} Projects service" caption-side="top"}

### {{site.data.keyword.compliance_short}}
{: #security-compliance-account-management-terra}

You can give users access to create, update, and delete resources for the {{site.data.keyword.compliance_short}} service in the account that you are assigned access.

| Roles         | Actions                                                                                                                                                    |
|---------------|------------------------------------|
| Viewer        | View available profiles and attachments   \n  \n View created resources such as scopes, credentials, or rules   \n  \n View global settings for the service |
| Operator      | Access the {{site.data.keyword.compliance_short}} dashboard to view current posture and results   \n  \n Create an audit log for monitoring compliance activity |
| Editor        | Create, update, or delete objects such as scopes, credentials, and collectors   \n  \n Update the parameter settings of a goal   \n  \n Create, update, or delete rules and templates   \n  \n Edit global admin settings for the service |
| Administrator | Perform all platform actions based on the resource that this role is being assigned, including assigning access policies to other users. |
| Manager       | Permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
| Reader        | Perform read-only actions within a service such as viewing service-specific resources. |
| Writer        | Permissions beyond the reader role, including creating and editing service-specific resources. |
{: caption="Roles and example actions for the {{site.data.keyword.compliance_short}} service" caption-side="top"}


### Software instance
{: #sw-instance-account-management-terra}

You can give users access to create, delete, or update a software instance. And, you can give users access to view the details page and the logs for the software instance.

| Roles         | Actions                            |
|---------------|------------------------------------|
| Viewer        | View the software instance details page |
| Operator      | Update a software instance   \n  \n View the details page for the software instance |
| Editor        | Create, delete, update a software instance   \n  \n View the details page for the software instance |
| Administrator | Create, delete, update a software instance   \n  \n View the details page for the software instance   \n  \n View the logs for the software instance   \n  \n Assign IAM permissions |
{: caption="Roles and example actions for the Software instance service" caption-side="top"}

### Support center
{: #support-center-account-management-terra}

You can give users access to manage support cases.

| Roles         | Actions                                                                       |
|---------------|-------------------------------------------------------------------------------|
| Viewer        |  View cases   \n  \n Search cases                                             |
| Operator      |  Not applicable                                                               |
| Editor        |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
| Administrator |  View cases   \n  \n Search cases   \n  \n Update cases   \n  \n Create cases |
{: caption="Roles and example actions for the Support Center service" caption-side="top"}

Assign users the viewer role on the user management service in addition to a support center access policy so the user can see all cases in the account regardless of user list visibility settings. If the user list visibility is set to be restricted, this can limit a user's ability to view, search, and manage support cases in an account that they didn't open themselves.
{: tip}

### User management
{: #user-management-account-management-terra}

You can give users access to view users in an account, invite and remove users, and view and update user profile settings.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View users in the account   \n  \n View user profile settings                                          |
| Operator      | View users in the account   \n  \n View user profile settings                                          |
| Editor        | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
| Administrator | View, invite, remove, and update users from the account   \n  \n View and update user profile settings |
{: caption="Roles and example actions for the User Management service" caption-side="top"}

The viewer role on the user management service is a role that is commonly assigned for users assigned a role to view or manage support cases. If an account owner restricts the visibility of the user list in the IAM settings, users can't see support cases that are opened by other users in the account. However, if they are assigned the viewer role for the user management service, the user list visibility setting doesn't affect the ability to view cases in the account.
{: tip}

### {{site.data.keyword.atracker_short}}
{: #activty-tracker-account-management-terra}

You can give users access to run platform actions.

| Roles         | Actions                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------|
| Viewer        | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Operator      | View {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Editor        | View, create, update, and delete {{site.data.keyword.atracker_short}} resources. |
| Administrator | View, create, update, and delete {{site.data.keyword.atracker_short}} resources.   \n  \n Assign access policies to manage {{site.data.keyword.atracker_short}} resources to other users in the account. |
{: caption="Roles and example actions for the {{site.data.keyword.atracker_short}} service" caption-side="top"}
