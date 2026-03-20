---
copyright:

  years: 2015, 2026
lastupdated: "2026-03-20"

keywords: invite, invite users, invitation access, vpn-only user, remove user, delete user, IBMid change, credentials, ID, new ID

subcollection: iam

---
{{site.data.keyword.attribute-definition-list}}

# Managing users in an account
{: #iamuserinv}

Use {{site.data.keyword.Bluemix}} Identity and Access Management (IAM) to manage users in your account. You can invite users, cancel invitations, remove a user from an account, or update a user's IBMid.
{: shortdesc}

All users must accept an invitation to become an active user within a new account. For more information, see [Canceling or resending pending invitations](/docs/account?topic=account-iamuserinv&interface=ui#pending-invitations)
{: important}

## Before you begin
{: #manage-users-access}

### Inviting users to an account
{: #invite-users-access}

To invite users and manage outstanding invitations, you must have at least one of the following types of access. Only users can invite others. If you use a service ID to authenticate, you can't invite new users to the account.

* Account owner
* An IAM access policy with the Editor role or higher on the user management account management service
* The Manage Users classic infrastructure permission to add users

Depending on your access level, you can invite new users and assign all or just some types of access.
{: note}

Before you can invite users by using Terraform, make sure that you have completed the following:
{: terraform}

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.
{: terraform}

### Removing users from an account
{: #remove-user-access}

Only account owners and users with the correct access can remove others. If you use a service ID to authenticate, you can't remove users from the account. The following access is required for removing users from an account:

* An Identity and access management (IAM) policy for the User management account management service with the Administrator role assigned.
* If you have classic infrastructure in your account, a user must have an IAM policy for the User management account management service with the Administrator role assigned and be an ancestor of the user in the classic infrastructure user hierarchy with the Manage user classic infrastructure permission assigned.

### Changing a user's IBMid
{: #change-ibm-id-access}

To change an IBMid, the replacement ID must already exist. If you're not sure if the new IBMid exists, users can go to [My IBM](https://myibm.ibm.com/) and click **Create an IBMid**. If you enter an email address that corresponds to a federated identity provider (IdP) domain, IBMid redirects you to that IdP's login page. First-time logins to {{site.data.keyword.IBM}} using a federated IdP triggers the creation of a new IBMid. Otherwise, follow the steps to create the ID. The email address that is used becomes the user's new replacement IBMid.



## Inviting users in the console
{: #invitations}
{: help}
{: support}
{: ui}

To invite users, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Users**.
1. Click **Invite users**.
1. Specify the email addresses of the users. If you are inviting more than one user with a single invitation, they are all assigned the same access.
   You can restrict membership to your account based on the domain of the users that are invited. This way, only users from a specific domain can be invited to the account. For more information, see [Restrict user domains for account invitations](/docs/account?topic=account-restrict-acct-invite).

Users cannot be automatically invited in enterprise-managed accounts and must be added manually.
{: note}

1. Add one or more of the access options that you manage. You must assign at least one access option. For any access options that you don't add and configure, the default value of **No access** is assigned. Depending on the options that you are authorized to manage, you can assign the following types of access:
   * Add users to access groups. Click **Add** for each access group that you want the users to belong to.
   * Manually assign users access. Expand the section to assign individual IAM access policies or classic infrastructure permissions.
      * Select **Classic infrastructure**, and then choose from the three permission sets.
      * Select a group of services like **All Identity and Access enabled services**, **All Account management services**, and **All IAM Account Management services**, or a specific service. Next, you can scope the access to the entire account or just one resource group. Then, select all roles that apply. To view what actions are mapped to each role, click the numbers listed next to each role.
         Some services support the use of advanced operators to grant access to resources that satisfy specific naming conventions. See [Assigning access by using wildcard policies](/docs/account?topic=account-wildcard) for more information.
      * Select **Account management**, and then choose from the all account management services option or select a specific service. Then, select all roles that apply.
1. Select **Add** to save the access assignment to the invitation.
1. After you add all the necessary access assignments, click **Invite**.

You can cancel an invitation for any users that are shown in a Processing or Pending state in the Status column of the [Users page](/iam/users). If an invited user did not receive an invitation, you can resend the invitation to any user in a Pending state. You can add more policies and permissions only after a user accepts the invitation.
{: note}

## Adding VPN-only users
{: #add-vpn-only}
{: ui}

Any user with the following permissions can add a VPN-only user:

- For classic infrastructure, you must have the Manage Users permission on the account.
- For IAM access, you must have the Administrator or Editor role on the user management account management service.

To add a VPN-only user, use the following steps:

1. On the Users page, click **Add VPN-only user**.
1. Enter the personal information details for the user.
1. Click **Save**.

## Inviting users by using the CLI
{: #cli-invite}
{: cli}

To invite users by using the CLI, run the following command:
```sh
ibmcloud account user-invite USER_EMAIL [--access-groups ACCESS_GROUP_1,ACCESS_GROUP_2...]
```
{: codeblock}

By using the CLI, you can choose not to assign access and work on assigning access later. For more information about the command parameters, see [**`ibmcloud account user-invite`**](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_user_invite).

## Inviting users by using the API
{: #api-invite}
{: api}

You can use the [API](https://cloud.ibm.com/apidocs/user-management#invite-users){: external} to invite users in bulk. All users that are included in a single invitation are assigned the same access. When you invite users by using the API, you enter emails in a comma-separated list with each entry that is surrounded by quotations. This example assigns access by adding the user to an access group.
``` bash
curl -X POST https://user-management.cloud.ibm.com/v2/accounts/987d4cfd77b04e9b9e1a6asdcc861234/users -H 'Authorization: Bearer <IAM_TOKEN>'
  -H 'Content-Type: application/json' -d '{
      "users": [
      {
        "email": "cloud_api_example_member@ibm.com",
        "account_role": "Member"
      }],
      "iam_policy": [{
        "type": "access",
        "roles": [{
          "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }],
        "resources": [{
          "attributes": [{
              "name": "accountId",
              "value": "987d4cfd77b04e9b9e1a6asdcc861234"
            },
            {
              "name": "resourceType",
              "value": "resource-group"
            },
            {
              "name": "resource",
              "value": "2c7449dd871049c29ec3a53853ce123e"
            }
          ]
        }]
      }],
      "access_groups":[
        "AccessGroupId-******-0f54-4d4f-89c2-e5fdc0b9a28c",
        "AccessGroupId-******-3087-4395-a382-a8e8ff9ccc23"
      ]
    }'
```
{: codeblock}
{: curl}

```java
InviteUser inviteUserModel = new InviteUser.Builder()
        .email(memberEmail)
        .accountRole("Member")
        .build();
Role roleModel = new Role.Builder()
        .roleId(viewerRoleId)
        .build();
Attribute attributeModel = new Attribute.Builder()
        .name("accountId")
        .value(accountId)
        .build();
Attribute attributeModel2 = new Attribute.Builder()
        .name("resourceGroupId")
        .value("*")
        .build();
Resource resourceModel = new Resource.Builder()
        .addAttributes(attributeModel)
        .addAttributes(attributeModel2)
        .build();
InviteUserIamPolicy inviteUserIamPolicyModel = new InviteUserIamPolicy.Builder()
        .type("access")
        .addRoles(roleModel)
        .addResources(resourceModel)
        .build();
InviteUsersOptions inviteUsersOptions = new InviteUsersOptions.Builder()
        .accountId(accountId)
        .addUsers(inviteUserModel)
        .addIamPolicy(inviteUserIamPolicyModel)
        .addAccessGroups(accessGroupId)
        .build();
Response<InvitedUserList> response = adminService.inviteUsers(inviteUsersOptions).execute();
InvitedUserList invitedUserList = response.getResult();
System.out.println(invitedUserList);
```
{: codeblock}
{: java}

```javascript
const inviteUserModel = {
  email: memberEmail,
  account_role: 'Member',
};
const roleModel = {
  role_id: viewerRoleId,
};
const attributeModel = {
  name: 'accountId',
  value: accountId,
};
const attributeModel2 = {
  name: 'resourceGroupId',
  value: '*',
};
const resourceModel = {
  attributes: [attributeModel, attributeModel2],
};
const inviteUserIamPolicyModel = {
  type: 'access',
  roles: [roleModel],
  resources: [resourceModel],
};
const params = {
  accountId: accountId,
  users: [inviteUserModel],
  iamPolicy: [inviteUserIamPolicyModel],
  accessGroups: [accessGroupId],
};
userManagementAdminService.inviteUsers(params)
  .then(res => {
    deleteUserId = res.result.resources[0].id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: codeblock}
{: javascript}

```python
invite_user_model = {
  'email': member_email,
  'account_role': 'Member'
}
role_model = {'role_id': viewer_role_id}
attribute_model = {'name': 'accountId', 'value': account_id}
attribute_model2 = {'name': 'resourceGroupId', 'value': '*'}
resource_model = {'attributes': [attribute_model, attribute_model2]}
invite_user_iam_policy_model = {
  'type': 'access',
  'roles': [role_model],
  'resources': [resource_model]
}
invite_user_response = user_management_admin_service.invite_users(
  account_id=account_id,
  users=[invite_user_model],
  iam_policy=[invite_user_iam_policy_model],
  access_groups=[access_group_id]
).get_result()
print(json.dumps(invite_user_response, indent=2))
```
{: codeblock}
{: python}

```go
inviteUserModel := &usermanagementv1.InviteUser{
  Email:       &memberEmail,
  AccountRole: core.StringPtr("Member"),
}
roleModel := &usermanagementv1.Role{
  RoleID: &viewerRoleID,
}
attributeModel := &usermanagementv1.Attribute{
  Name:  core.StringPtr("accountId"),
  Value: &accountID,
}
attributeModel2 := &usermanagementv1.Attribute{
  Name:  core.StringPtr("resourceGroupId"),
  Value: core.StringPtr("*"),
}
resourceModel := &usermanagementv1.Resource{
  Attributes: []usermanagementv1.Attribute{*attributeModel, *attributeModel2},
}
inviteUserIamPolicyModel := &usermanagementv1.InviteUserIamPolicy{
  Type:      core.StringPtr("access"),
  Roles:     []usermanagementv1.Role{*roleModel},
  Resources: []usermanagementv1.Resource{*resourceModel},
}
inviteUsersOptions := &usermanagementv1.InviteUsersOptions{
  AccountID:    &accountID,
  Users:        []usermanagementv1.InviteUser{*inviteUserModel},
  IamPolicy:    []usermanagementv1.InviteUserIamPolicy{*inviteUserIamPolicyModel},
  AccessGroups: []string{accessGroupID},
}
invitedUserList, response, err := userManagementAdminService.InviteUsers(inviteUsersOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(invitedUserList, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}

You can assign access to a group of services. To assign access to **All Identity and Access enabled services**, specify `serviceType` for the `name` attribute, and use the `value` `service`. To assign access to **All Account Management services**, specify `serviceType` for the `name` attribute, and use the `value` `platform_service`. To assign access to the subset of account management services **All IAM Account Management services**, specify `service_group_id` for the `name` attribute, and use the `value` `IAM`.
{: tip}

## Inviting users by using Terraform
{: #terraform-invite}
{: terraform}

You can invite users to your {{site.data.keyword.cloud_notm}} account by using Terraform.

1. Create an argument in your `main.tf` file. The following example invites users by using the `ibm_iam_user_invite` resource, where `users` are the list of user email IDs to invite.
   ```terraform
   resource "ibm_iam_user_invite" "invite_user" {
    users = ["test@in.ibm.com"]
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_user_invite){: external} page.
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

## Canceling or resending pending invitations
{: #pending-invitations}
{: ui}

After inviting new users to join your account, {{site.data.keyword.cloud_notm}} requires all except VPN-only users to accept the invitation to become an active user in your account.

The invitation expires after 30 days. New users to {{site.data.keyword.cloud_notm}} can accept an invitation only by using the invitation link that they received through email.
{: note}

You can cancel an invitation for any users that are shown in a Processing or Pending state in the Status column of the [Users page](/iam/users). If an invited user did not receive an invitation, you can resend the invitation to any user in a Pending state.
1. Go to the [Users page](/iam/users).
1. Locate the row for the user in `Processing` or `Pending` state.
1. Click the **Actions** icon ![More Actions icon](../icons/action-menu-icon.svg "Actions"), then choose to **Resend invite** or **Cancel invite**.

## Accepting invitations in the console
{: #accepting-invitations-ui}
{: ui}

If the invited user is already a member of {{site.data.keyword.cloud_notm}}, they receive an invitation link in their notifications and by email. On the [Notifications page](https://cloud.ibm.com/user/notifications){: external}, users can use the search field to locate an invitation or filter by the notification type called `account`. For more information, see [Managing invitation notifications](/docs/account?topic=account-email-prefs#invite-notifications) and [Viewing notifications](/docs/account?topic=account-viewing-cloud-status#view-notifications).

## Accepting invitations by using the CLI
{: #cli-accepting}
{: cli}

If the invited user is already a member of {{site.data.keyword.cloud_notm}}, they can accept invitations by using the CLI. In the following [**`ibmcloud login`**](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) command, the `ACCOUNT_ID` is the ID of the targeted account that the user is invited to join.
```sh
ibmcloud login -c ACCOUNT_ID --accept
```
{: codeblock}

## Accepting invitations by using the API
{: #api-accepting}
{: api}

If the invited user is already a member of {{site.data.keyword.cloud_notm}}, they can accept invitations by using the API. In the following example, the `ACCOUNT_ID` is the ID of the targeted account that the user is invited to join and the `IAM_TOKEN` belongs to the invitee.
```curl
curl -X POST \
  'https://iam.cloud.ibm.com/v2/users/accept' \
  --header 'Authorization: Bearer <IAM_TOKEN>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    "account_id": "<ACCOUNT ID>"
  }
```
{: codeblock}

## Removing a user from an account by using the console
{: #remove-user-acount-ui}
{: ui}

When you remove a user from an account, the user can no longer log in to the console, switch to your account, or access account resources. Removing a user from an account doesn't delete the IBMid for the user.

To remove a user from an account, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Users**.
2. From the row of the user that you want to remove, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Remove user**.

Any resources that are created by the user remain in the account, but any {{site.data.keyword.cloud_notm}} API keys that the user created are removed. The user no longer has access to work with the resources they created. The account owner or an administrator for the service or service instance can assign other users to work with the resources, or delete them from the account.

If you get an error message that states a classic infrastructure user can't be removed, make sure that any descendants in the user hierarchy for that user are [assigned a new parent](/docs/iam?topic=iam-user-setting#update-parent), [disabled in the account](/docs/account?topic=account-status), or deleted. Then, you can try again.
{: tip}

As an alternative to removing a user from your account, you can assign them an access policy with a temporary time-based condition. This way, the user can log in to the console and view the account in their account list, but can't access resources in the account before the policy begins or after the policy expires. For more information, see [Creating a temporary time-based condition](/docs/iam?topic=iam-time-based&interface=api#iam-time-based-temp-api).

## Removing a user from an account by using the CLI
{: #remove-user-acount-cli}
{: cli}

To remove a user from an account, run the following command:

```bash
ibmcloud account user-remove USER_ID [-c ACCOUNT_ID] [-f, --force]
```
{: codeblock}

For command options, see [Managing accounts and users](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_user_remove) CLI commands.

## Removing a user from an account by using the API
{: #remove-user-acount-api}
{: api}

To remove a user from an account, call the [User Management API](https://cloud.ibm.com/apidocs/user-management?code=java#remove-user) as shown in the following sample request.

Replace variables with the user's IAM ID. You must use a user token for authorization. Service IDs can't remove users from an account.

```bash
curl -X DELETE https://user-management.cloud.ibm.com/v2/accounts/987d4cfd77b04e9b9e1a6asdcc861234/users/IBMid-1000000000 -H 'Authorization: Bearer <IAM_TOKEN>' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
RemoveUserOptions removeUserOptions = new RemoveUserOptions.Builder()
  .accountId(accountId)
  .iamId(deleteUserId)
  .build();
service.removeUser(removeUserOptions).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  accountId: accountId,
  iamId: deleteUserId,
};
userManagementAdminService.removeUser(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: codeblock}
{: javascript}

```python
response = user_management_admin_service.remove_user(
  account_id=account_id,
  iam_id=delete_user_id,
).get_result()
print(json.dumps(response, indent=2))
```
{: codeblock}
{: python}

```go
removeUserOptions := userManagementService.NewRemoveUserOptions(
  accountID,
  deleteUserID,
)
response, err := userManagementAdminService.RemoveUser(removeUserOptions)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

You can also remove a user by their user ID or by their email address and realm. Either the user ID or email and realm is required. For more information, see [Remove user from account by user ID or email](/apidocs/user-management#remove-user-by-email-or-id).
```bash
curl -X DELETE https://user-management.cloud.ibm.com/v2/accounts/987d4cfd77b04e9b9e1a6asdcc861234/users?user_id=user%40ibm.com&email=user.email%40ibm.com&realm=ibmid -H 'Authorization: Bearer <IAM_TOKEN>' -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

## Changing a user's IBMid by using the console
{: #change-ibm-id}
{: ui}

As an account owner, you can update a user's IBMid. The new IBMid that you use to replace the current IBMid must already exist.
The IBMid you're replacing is removed from the account. If you need the existing IBMid to continue to be a member of the account, you must invite the user again and reestablish their access.

Account owners can't change their own IBMid.
{: note}

After the user ensures that the new IBMid exists, complete the following steps to change the user's IBMid:
1. Go to **Manage** > **Access (IAM)** > **Users** in the {{site.data.keyword.cloud}} console, and select the user whose IBMid you want to update.
2. In the **Details** section, click **Update IBMid**.
3. Enter the new IBMid, and click **Update**.

The user can now log in to ibm.com with their new IMBid and continue working in the {{site.data.keyword.cloud_notm}} account with the access assigned to their previously used IBMid.

