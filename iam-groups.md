---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-31"

keywords: access groups, access group, create group, assign access to group, administrator, administrator role, streamlined access, efficient permissions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Streamlined access management with access groups
{: #groups}

Organize users, service IDs, and trusted profiles into access groups for efficient permission management. Assign fine-grained policies once to the entire group to implement least privilege at scale.
{: shortdesc}

An access group can be created to organize a set of users, service IDs, and trusted profiles into a single entity that makes it easy for you to assign access. You can assign a single policy to the group instead of assigning the same access multiple times for an individual user or service ID.

Access groups are assigned policies that grant roles and permissions to the members of that group. Members of an access group can include multiple identity types, like users, service IDs, and trusted profiles. The members inherit the policies, roles, and permissions that are assigned to the access group, and also keep the roles that they are assigned individually.

For example, if a user is assigned the `viewer` role on the billing service and they are added to an access group that has the `publisher` role on the catalog management service, they keep their `viewer` role even though that isn't part of the access group permissions.

To make assigning and managing access even easier, you can set up resource groups to organize a set of resources that you want a group of users to have access to. When your resource group is set up, you can assign a policy that gives access to all resources within that group instead of creating access policies for individual service instances within your account.
{: tip}


## Before you begin
{: #prereq-create-groups}
{: ui}

To manage or create new access groups, you must have the following type of access:

* Administrator or editor on the IAM Access Groups account management service in the account
* Administrator or editor for the All Account Management services
* You must be the account owner

Additionally, an administrator or editor can be assigned access to manage an individual group by creating an access policy where the resource is the Access group ID. For more information about access policies and roles for the IAM Access Groups service, see [IAM access](/docs/iam?topic=iam-userroles#userroles).

## Before you begin
{: #prereq-create-groups-tf}
{: terraform}

Before you can set up access groups by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

## Creating an access group in the console
{: #create_ag}
{: ui}
{: support}
{: help}

A unique name is required to differentiate access groups in the account. To create an access group, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Access Groups**.
1. Click **Create**.
1. Enter a unique name to identify your access group, an optional description, and click **Create**.

Next, continue to set up your groups by adding users, service IDs, or trusted profiles. You can add users manually or by [creating dynamic rules](/docs/iam?topic=iam-rules&interface=ui). Or, you can start assigning the group access, and decide who you want to add to the access group later.

You can delete a group by selecting the **Remove group** option. When you remove a group from the account, you are removing all users and service IDs from the group and all access that is assigned to the group.
{: note}

## Creating an access group by using the CLI
{: #create_ag_cli}
{: cli}

To create an access group by using the CLI, you can use the [ibmcloud iam access-group-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```bash
ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
{: codeblock}

A unique name is required to differentiate access groups in the account.
{: note}

## Creating an access group by using the API
{: #create_ag_api}
{: api}

You can programmatically create access groups by calling the [{{site.data.keyword.iamlong}} (IAM) Access Groups API](/apidocs/iam-access-groups#create-access-group){: external} as shown in the following sample request. The example creates an access group for managers in the account:

```bash
curl -X POST -H "Authorization: Bearer {iam_token}" \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{ "name": "Managers", "description": "Group for managers" }' \
"{base_url}/groups?account_id={account_id}"
```
{: curl}
{: codeblock}

```java
CreateAccessGroupOptions createAccessGroupOptions = new CreateAccessGroupOptions.Builder()
  .accountId(testAccountId)
  .name("Managers")
  .description("Group for managers")
  .build();

Response<Group> response = service.createAccessGroup(createAccessGroupOptions).execute();
Group group = response.getResult();

System.out.println(group);
```
{: java}
{: codeblock}

```javascript
const params = {
  accountId: testAccountId,
  name: 'Managers',
  description: 'Group for managers'
};

iamAccessGroupsService.createAccessGroup(params)
  .then(res => {
    testGroupId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
group = iam_access_groups_service.create_access_group(
  account_id=test_account_id,
  name='Managers',
  description='Group for managers'
).get_result()

print(json.dumps(group, indent=2))
```
{: python}
{: codeblock}

```go
createAccessGroupOptions := iamAccessGroupsService.NewCreateAccessGroupOptions(testAccountID, "Managers")
createAccessGroupOptions.SetDescription("Group for managers")
group, response, err := iamAccessGroupsService.CreateAccessGroup(createAccessGroupOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(group, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}

A unique name is required to differentiate access groups in the account.
{: note}


## Creating an access group by using Terraform
{: #create-ag-terraform}
{: terraform}

Use the following steps to create access groups by using Terraform:

1. Create an argument in your `main.tf` file. The following example creates an access group by using the `ibm_iam_access_group` resource, where `name` is a unique name to identify the access group.

   ```terraform
   resource "ibm_iam_access_group" "accgrp" {
    name        = "test"
    description = "New access group"
   }
   ```
   {: codeblock}

   You can also specify the description of the access group on the `description` option. For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group){: external} page.

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

## Assigning access to a group in the console
{: #access_ag}
{: ui}

After you set up your group with users and service IDs, you can assign a common access policy to the group. Remember, any policy that you set for the group applies to all entities within the group. For example, assigning access policies to an access group delegates the ability to grant or revoke access to users, service-ids, or trusted profiles to the administrators of that access group.

Administrator access to everything in the account includes the ability to revoke access for other users with the administrator role.
{: important}

Use the following steps to assign access to a group in the console:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Access Groups**.
1. For the group that you want to assign access, select the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and click **Assign access**.
1. You can assign access to only resources that you manage. You must assign at least one access option. For any access options that you don't add and configure, the default value of **No access** is assigned. Depending on the options that you are authorized to manage, you can assign the following types of access:

     * A group of services, like **All Identity and Access enabled services**, **All Account Management services**, or **All IAM Account Management services**.
     * A specific service

1. Next, you can scope the access to all resources or specific resources based on selected resource attributes like access management tags, location, or resource group.
1. Select all roles that apply. To view what actions are mapped to each role, click the numbers listed next to each role. Some services support the use of advanced operators to grant access to resources that satisfy specific naming conventions. See [Assigning access by using wildcard policies](/docs/iam?topic=iam-wildcard) for more information.
1. Click **Review**.
1. Click **Add** to add your policy configuration to your policy summary.
1. Click **Assign**.

You can also assign access by using access management tags. For more information, see [Controlling access to resources by using tags](/docs/account?topic=account-access-tags-tutorial).
{: tip}

## Assigning access to a group by using the CLI
{: #access_ag_cli}
{: cli}

To create an access group policy by using the CLI, you can use the [ibmcloud iam access-group-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command.

```bash
ibmcloud iam access-group-policy-create GROUP_NAME {-f, --file @JSON_FILE | --roles ROLE_NAME1,ROLE_NAME2... [--service-name SERVICE_NAME] [--service-instance SERVICE_INSTANCE] [--region REGION] [--resource-type RESOURCE_TYPE] [--resource RESOURCE] [--resource-group-name RESOURCE_GROUP_NAME] [--resource-group-id RESOURCE_GROUP_ID]}
```
{: codeblock}

## Assigning access to a group by using the API
{: #access_ag_api}
{: api}

You can programmatically assign access to a group by calling the [{{site.data.keyword.iamlong}} (IAM) Policy Management API](/apidocs/iam-policy-management#create-policy){: external} as shown in the following sample request. The example assigns an access group `Editor` role for an instance of a service:

```bash
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' \
-H 'Authorization: Bearer $TOKEN' \
-H 'Content-Type: application/json' \
-d '{
  "type": "access",
  "description": "Editor role for SERVICE_NAME's RESOURCE_NAME",
  "subjects": [
    {
      "attributes": [
        {
          "name": "access_group_id",
          "value": "exampleAccessGroupId"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:iam::::role:Editor"
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
          "value": "$SERVICE_NAME"
        },
        {
          "name": "resource",
          "value": "$RESOURCE_NAME",
          "operator": "stringEquals"
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
        .name("access_group_id")
        .value(exampleAccessGroupId)
        .build();

PolicySubject policySubjects = new PolicySubject.Builder()
        .addAttributes(subjectAttribute)
        .build();

PolicyRole policyRoles = new PolicyRole.Builder()
        .roleId("crn:v1:bluemix:public:iam::::role:Editor")
        .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
        .name("accountId")
        .value(exampleAccountId)
        .operator("stringEquals")
        .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
        .name("serviceType")
        .value("service")
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
        name: 'access_group_id',
        value: exampleAccessGroupId,
      },
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:iam::::role:Editor',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: exampleAccountId,
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceType',
  value: 'service',
  operator: 'stringEquals',
};
const policyResources = [
  {
    attributes: [accountIdResourceAttribute, serviceNameResourceAttribute],
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
  attributes=[SubjectAttribute(name='access_group_id', value=exampleAccessGroupId)])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:iam::::role:Editor')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
  name='serviceType', value='service')
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
  Name:  core.StringPtr("access_group_id"),
  Value: &exampleAccessGroupId,
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:iam::::role:Editor"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr(exampleAccountID),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceType"),
  Value:    core.StringPtr("service"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute}
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

You can assign access to a group of services. To assign access to **All Identity and Access Enabled services**, specify `serviceType` for the `name` attribute, and use the `value` `service`. To assign access to **All Account Management services**, specify `serviceType` for the `name` attribute, and use the `value` `platform_service`. To assign access to the subset of account management services **All IAM Account Management services**, specify `service_group_id` for the `name` attribute, and use the `value` `IAM`.
{: tip}

## Assigning access to a group by using Terraform
{: #access_ag_terraform}
{: terraform}

After you set up your group, use the following steps to assign access to it by using Terraform.

1. Create an argument in your `main.tf` file. The following examples create an IAM policy that grants members of the access group the IAM `Viewer` platform role to all IAM-enabled services by using the `ibm_iam_access_group_policy` resource. You must have an existing IAM ID of an access group in order to complete the task.

   ```terraform
   resource "ibm_iam_access_group" "accgrp" {
    name = "test"
   }
   ```
   {: codeblock}

   ```terraform
   resource "ibm_iam_access_group_policy" "policy" {
    access_group_id = ibm_iam_access_group.accgrp.id
    roles           = ["Viewer"]
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group_policy){: external} page.

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


## Adding members to an access group in the console
{: #add-users-ag}
{: ui}

Members can be users, service IDs, and trusted profiles.

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Access Groups**.
1. Click on the access group that you created.
1. Add members.
   1. Click **Add users**.
   1. Click **Service IDs > Add Service IDs**.
   1. Click **Trusted profiles > Add trusted profiles**.

   If you don't see the button to add members, you might not have access. Review the [access requirements](/docs/iam?topic=iam-groups&interface=ui#prereq-create-groups) and contact your account administrator for access.
   {: note}

1. Select the users, service IDs, or trusted profiles that you want to add to the group and click **Add to group**.

Members that you add to the group can use the level of access that you assign to the group.

## Adding members to an access group by using the CLI
{: #add-users-ag-cli}
{: cli}

Members can be users, service IDs, and trusted profiles. Members that you add to the group can use the level of access that you assign to the group.

1. Get the users, service IDs, or trusted profiles in your account. Note the details that are returned for the member you want to add to the access group.

   [Get all users](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_users):

    ```bash
   ibmcloud account users [-c, --account-id ACCOUNT_ID]
   ```
   {: codeblock}

   [List all service IDs](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_service_ids):

   ```bash
   ibmcloud iam service-ids [--uuid]
   ```
   {: codeblock}

   [Get all trusted profiles](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_trusted_profiles):

    ```bash
   ibmcloud iam trusted-profiles [--id | --output FORMAT] [-q, --quiet]
   ```
   {: codeblock}

1. Add members to the access group:

    Use the [ibmcloud iam access-group-user-add](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create) command to add users to an access group. The following example adds user `name@example.com` to access group `example_group` by using the CLI.

    ```bash
    ibmcloud iam access-group-user-add example_group name@example.com
    ```
    {: codeblock}

    Use the [ibmcloud iam access-group-service-id-add](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_service_id_add) command to add service IDs to an access group. The following example adds service ID `example-service` to access group `example_group`:

    ```bash
    ibmcloud iam access-group-service-id-add example_group example-service
    ```
    {: codeblock}

    Use the [ibmcloud iam access-group-trusted profile-add](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_trusted_profile_add) command to add trusted profiles to an access group. The following example adds service ID `PROFILE_ID` to access group `example_group`:

    ```bash
    ibmcloud iam access-group-trusted-profile-add GROUP_NAME (PROFILE_NAME | PROFILE_ID) [PROFILE_NAME2 | PROFILE_ID2...] [--output FORMAT] [-q, --quiet]
    ```
{: codeblock}

## Adding members to an access group by using the API
{: #add-users-ag-api}
{: api}

Members can be users, service IDs, and trusted profiles.

1. List the users, service IDs, or trusted profiles in your account as shown in the following example request. Note the IBMid, service ID or trusted profile ID that is returned for the member that you want to add to the access group.

   [List users](/apidocs/user-management?code=go#list-users):

    ```bash
    curl -X GET https://user-management.cloud.ibm.com/v2/accounts/987d4cfd77b04e9b9e1a6asdcc861234/users -H 'Authorization: Bearer <IAM_TOKEN>'
    ```
    {: codeblock}
    {: curl}

    ```java
    ListUsersOptions listUsersOptions = new ListUsersOptions.Builder()
      .accountId(accountId)
      .build();

    UsersPager pager = new UsersPager(userManagementService, listUsersOptions);
    List<UserProfile> allResults = new ArrayList<>();
    while (pager.hasNext()) {
      List<UserProfile> nextPage = pager.getNext();
      allResults.addAll(nextPage);
    }

    System.out.println(GsonSingleton.getGson().toJson(allResults));
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      accountId: accountId,
    };

    const allResults = [];
    try {
      const pager = new UserManagementV1.UsersPager(userManagementService, params);
      while (pager.hasNext()) {
        const nextPage = await pager.getNext();
        expect(nextPage).not.toBeNull();
        allResults.push(...nextPage);
      }
      console.log(JSON.stringify(allResults, null, 2));
    } catch (err) {
      console.warn(err);
    }
    ```
    {: codeblock}
    {: javascript}

    ```python
    all_results = []
    pager = UsersPager(
      client=user_management_service,
      account_id=account_id,
    )
    while pager.has_next():
      next_page = pager.get_next()
      assert next_page is not None
      all_results.extend(next_page)

    print(json.dumps(all_results, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    listUsersOptions := &usermanagementv1.ListUsersOptions{
      AccountID: &accountID,
    }

    pager, err := userManagementService.NewUsersPager(listUsersOptions)
    if err != nil {
      panic(err)
    }

    var allResults []usermanagementv1.UserProfile
    for pager.HasNext() {
      nextPage, err := pager.GetNext()
      if err != nil {
        panic(err)
      }
      allResults = append(allResults, nextPage...)
    }
    b, _ := json.MarshalIndent(allResults, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

   [List service IDs](/apidocs/iam-identity-token-api?code=go#list-service-ids):

    ```bash
    curl -X GET 'https://iam.cloud.ibm.com/v1/serviceids?account_id=ACCOUNT_ID&name=My-serviceID' -H 'Authorization: Bearer TOKEN' -H 'Content-Type: application/json'
    ```
    {: codeblock}
    {: curl}

    ```java
    ListServiceIdsOptions listServiceIdsOptions = new ListServiceIdsOptions.Builder()
        .accountId(accountId)
        .name(serviceIdName)
        .build();

    Response<ServiceIdList> response = service.listServiceIds(listServiceIdsOptions).execute();
    ServiceIdList serviceIdList = response.getResult();

    System.out.println(serviceIdList);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      accountId: accountId,
      name: serviceIdName,
    };

    try {
      const res = await iamIdentityService.listServiceIds(params)
      console.log(JSON.stringify(res.result, null, 2));
    } catch (err) {
      console.warn(err);
    }
    ```
    {: codeblock}
    {: javascript}

    ```python
    service_id_list = iam_identity_service.list_service_ids(
      account_id=account_id, name=serviceid_name
    ).get_result()

    print(json.dumps(service_id_list, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    listServiceIdsOptions := iamIdentityService.NewListServiceIdsOptions()
    listServiceIdsOptions.SetAccountID(accountID)
    listServiceIdsOptions.SetName(serviceIDName)

    serviceIDList, response, err := iamIdentityService.ListServiceIds(listServiceIdsOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(serviceIDList, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}


   [List trusted profiles](/apidocs/iam-identity-token-api?code=python#list-profiles):

    ```bash
    curl -X GET 'https://iam.cloud.ibm.com/v1/profiles?account_id=ACCOUNT_ID' -H 'Authorization: Bearer TOKEN' -H 'Accept: application/json'
    ```
    {: codeblock}
    {: curl}

    ```java
    ListProfilesOptions listProfilesOptions = new ListProfilesOptions.Builder()
        .accountId(accountId)
        .includeHistory(false)
        .build();

    Response<TrustedProfilesList> response = service.listProfiles(listProfilesOptions).execute();
    TrustedProfilesList profiles = response.getResult();

    System.out.println(profiles);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      accountId: accountId,
      includeHistory: false,
    };

    try {
      const res = await iamIdentityService.listProfiles(params);
      console.log(JSON.stringify(res.result, null, 2));
    } catch (err) {
      console.warn(err);
    }
    ```
    {: codeblock}
    {: javascript}

    ```python
    profile_list = iam_identity_service.list_profiles(account_id=account_id, include_history=True).get_result()

    print(json.dumps(profile_list, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    listProfilesOptions := iamIdentityService.NewListProfilesOptions(accountID)
    listProfilesOptions.SetIncludeHistory(false)

    trustedProfiles, response, err := iamIdentityService.ListProfiles(listProfilesOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(trustedProfiles, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

1. Add members to the access group by calling the [IAM Access Groups](/apidocs/iam-access-groups?code=go#add-members-to-access-group) API as shown in the following example request.

   The type of member must be `user`, `service` or `profile`.
   {: tip}

    ```bash
    curl -X PUT --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "members": [ { "iam_id": "IBMid-user1", "type": "user" }, { "iam_id": "iam-ServiceId-123", "type": "service" }, { "iam_id": "iam-Profile-123", "type": "profile" } ] }' "{base_url}/v2/groups/{access_group_id}/members"
    ```
    {: codeblock}
    {: curl}

    ```java
    AddGroupMembersRequestMembersItem member1 = new AddGroupMembersRequestMembersItem.Builder()
      .iamId("IBMid-user1")
      .type("user")
      .build();
    AddGroupMembersRequestMembersItem member2 = new AddGroupMembersRequestMembersItem.Builder()
      .iamId("iam-ServiceId-123")
      .type("service")
      .build();
      AddGroupMembersRequestMembersItem member3 = new AddGroupMembersRequestMembersItem.Builder()
      .iamId(testProfileId)
      .type("profile")
      .build();
    AddMembersToAccessGroupOptions addMembersToAccessGroupOptions = new AddMembersToAccessGroupOptions.Builder()
      .accessGroupId(testGroupId)
      .addMembers(member1)
      .addMembers(member2)
      .addMembers(member3)
      .build();
    Response<AddGroupMembersResponse> response = iamAccessGroupsService.addMembersToAccessGroup(addMembersToAccessGroupOptions).execute();
    AddGroupMembersResponse addGroupMembersResponse = response.getResult();

    System.out.println(addGroupMembersResponse);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const groupMember1 = {
      iam_id: 'IBMid-user1',
      type: 'user',
    };
    const groupMember2 = {
      iam_id: 'iam-ServiceId-123',
      type: 'service',
    };
    var groupMember3 = {
      iam_id: profileId,
      type: 'profile',
    }

    const params = {
      accessGroupId: testGroupId,
      members: [groupMember1, groupMember2, groupMember3],
    };

    try {
      const res = await iamAccessGroupsService.addMembersToAccessGroup(params);
      console.log(JSON.stringify(res.result, null, 2));
    } catch (err) {
      console.warn(err);
    }
    ```
    {: codeblock}
    {: javascript}

    ```python
    member1 = AddGroupMembersRequestMembersItem(iam_id='IBMid-user1', type='user')
    member2 = AddGroupMembersRequestMembersItem(iam_id='iam-ServiceId-123', type='service')
    member3 = AddGroupMembersRequestMembersItem(iam_id=test_profile_id, type='profile')
    members = [member1, member2, member3]

    response = iam_access_groups_service.add_members_to_access_group(
      access_group_id=test_group_id,
      members=members,
    )
    add_group_members_response = response.get_result()

    print(json.dumps(add_group_members_response, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    groupMembers := []iamaccessgroupsv2.AddGroupMembersRequestMembersItem{
      iamaccessgroupsv2.AddGroupMembersRequestMembersItem{
        IamID: core.StringPtr("IBMid-user1"),
        Type:  core.StringPtr("user"),
      },
      iamaccessgroupsv2.AddGroupMembersRequestMembersItem{
        IamID: core.StringPtr("iam-ServiceId-123"),
        Type:  core.StringPtr("service"),
      },
      iamaccessgroupsv2.AddGroupMembersRequestMembersItem{
        IamID: core.StringPtr(testProfileID),
        Type:  core.StringPtr("profile"),
      },
    }

    addMembersToAccessGroupOptions := iamAccessGroupsService.NewAddMembersToAccessGroupOptions(
      accessGroupIDLink,
    )
    addMembersToAccessGroupOptions.SetMembers(groupMembers)

    addGroupMembersResponse, response, err := iamAccessGroupsService.AddMembersToAccessGroup(addMembersToAccessGroupOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(addGroupMembersResponse, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

Members that you add to the group can use the level of access that you assign to the group.


## Adding members to an access group by using Terraform
{: #add-users-ag-terra}
{: terraform}

Members can be users, service IDs, and trusted profiles.

1. Create an argument in your `main.tf` file. The following example adds a service ID, trusted profile, and a user with the ID `user@ibm.com` to an access group.


   ```terraform
   resource "ibm_iam_access_group_members" "accgroupmem" {
     access_group_id = ibm_iam_access_group.accgroup.id
     ibm_ids         = ["user@ibm.com"]
     iam_service_ids = [ibm_iam_service_id.serviceID.id]
     iam_profile_ids = [ibm_iam_trusted_profile.profileID.id]
   }
   ```
   {: codeblock}


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


Members that you add to the group can use the level of access that you assign to the group.
