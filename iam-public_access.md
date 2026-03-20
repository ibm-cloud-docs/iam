---

copyright:

  years: 2019, 2026
lastupdated: "2026-03-20"

keywords: public access, anonymous access, users, service IDs, public access group, enable, disable, manage, IAM

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Managing public access to resources
{: #public}

By default, all users and service IDs in an account are members of the Public Access group in your account. Assigning an access policy to the access group opens access to that resource to anyone whether they're a member of your account or not because authentication is no longer required. However, sometimes you might want to help ensure that there is never public access that is allowed to your account resources, which you control by disabling public access at the account level.
{: shortdesc}

To manage public access, you must be an administrator of the [IAM Access Groups service](/docs/account?topic=account-account-services#access-groups-account-management) in the account.

## Assigning public access to resources
{: #public_policy}

When public access is enabled in the account, you can create a policy to define the resources that all members of the Public Access group can access.

To enable public access, complete the following steps:
1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)** >**Settings** > **Public access**.
1. Enable the **Public access group**.
1. Click **Yes** to confirm.

### Assigning access in the console
{: #public-access-console}
{: ui}

To create a policy, you must have administrator access on the resource.

{{site.data.keyword.cos_full}} is used as the example as it is the only supported resource type for public access now. As an example, the following section describes how to assign public access to an {{site.data.keyword.cos_short}} bucket that is named `mybucket123`.

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Access groups**.
2. Click the name of the public access group > **Assign access**.
3. Select **{{site.data.keyword.cos_short}}** from the **Services** list.
4. Select the specific instance from the **Service instance** list.
5. Enter `bucket` for the resource type.
6. Enter `mybucket123` for the resource ID.
7. Select the service access role, and click **Assign**.
8. Confirm that you want to assign the public access policy to the resource, and click **Assign**.

### Assigning access by using the CLI
{: #public-access-cli}
{: cli}

To assign access for the Public Access group, run the **`ibmcloud iam access-group-policy-create`** command. In the command example, the policy details are specified in a JSON file. Switch to the API instructions for an example of what to include in the JSON file.

```sh
ibmcloud iam access-group-policy Public Access -f @policy.json
```
{: pre}

For more information about the command options, see [`ibmcloud iam access-group-policy-create`](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_access_group_policy_create).

### Assigning access by using the API
{: #public-access-api}
{: api}

The following request example creates a policy for the Public Access group.

```bash
curl -X POST \
'https://iam.cloud.ibm.com/v1/policies' \
-H 'Authorization: $TOKEN' \
-H 'Content-Type: application/json' \
-d '{
  "type": "access",
  "subjects": [
    {
      "attributes": [
        {
          "name": "access_group_id",
          "value": "AccessGroupId-PublicAccess"
        }
      ]
    }
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
          "value": "$SERVICE_NAME"
        },
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
        .value(AccessGroupId-PublicAccess)
        .build();

PolicySubject policySubjects = new PolicySubject.Builder()
        .addAttributes(subjectAttribute)
        .build();

PolicyRole policyRoles = new PolicyRole.Builder()
        .roleId("crn:v1:bluemix:public:iam::::role:Administrator")
        .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
        .name("accountId")
        .value(exampleAccountId)
        .operator("stringEquals")
        .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
        .name("serviceName")
        .value("exampleServiceName")
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
        value: AccessGroupId-PublicAccess,
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
  value: exampleAccountId,
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: 'exampleServiceName',
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
  attributes=[SubjectAttribute(name='access_group_id', value=AccessGroupId-PublicAccess)])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:iam::::role:Administrator')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='exampleServiceName')
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
  Value: &AccessGroupId-PublicAccess,
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:iam::::role:Administrator"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr(exampleAccountID),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("exampleServiceName"),
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

For more information, see [Create a policy](https://cloud.ibm.com/apidocs/iam-policy-management?code=go#create-policy){: external}.

## Disabling public access to resources
{: #disable-public-access}

When you disable public access, all existing policies for the Public Access group are deleted, which revokes the previously allowed access. You also can't create or modify any policies for the Public Access group.

### Disabling access in the console
{: #disable-public-ui}
{: ui}

To disable public access for the account, complete the following steps:

1. Go to **Manage** > **Access (IAM)** > **Settings** in the {{site.data.keyword.cloud_notm}} console.
1. Click Public access and disable the **Public access group**.

### Disabling access by using the CLI
{: #disable-public-cli}
{: cli}

This action can be done only through the UI or API. To see the steps, switch to the UI or API instructions.

### Disabling access by using the API
{: #disable-public-api}
{: api}

The following request example disables public access for the account.

```bash
curl -X PATCH \
'https://iam.cloud.ibm.com/v2/groups/settings?account_id=<account_id>' \
-H 'Authorization: $TOKEN' \
-H 'Content-Type: application/json' \
-d '{
  "public_access_enabled": false
}'
```
{: curl}
{: codeblock}

```java
UpdateAccountSettingsOptions updateAccountSettingsOptions = new UpdateAccountSettingsOptions.Builder()
  .accountId(testAccountId)
  .publicAccessEnabled(false)
  .build();

Response<AccountSettings> response = service.updateAccountSettings(updateAccountSettingsOptions).execute();
AccountSettings accountSettings = response.getResult();

System.out.println(accountSettings);
```
{: java}
{: codeblock}

```javascript
const params = {
  accountId: testAccountId,
  publicAccessEnabled: false,
};

iamAccessGroupsService.updateAccountSettings(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
account_settings = iam_access_groups_service.update_account_settings(
  account_id=test_account_id,
  public_access_enabled=False
).get_result()

print(json.dumps(account_settings, indent=2))
```
{: python}
{: codeblock}

```go
updateAccountSettingsOptions := iamAccessGroupsService.NewUpdateAccountSettingsOptions(testAccountID)
updateAccountSettingsOptions.SetPublicAccessEnabled(false)
accountSettings, response, err := iamAccessGroupsService.UpdateAccountSettings(updateAccountSettingsOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(accountSettings, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}

For more information, see [Update account settings](https://cloud.ibm.com/apidocs/iam-access-groups#update-account-settings){: external}.
