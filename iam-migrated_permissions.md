---

copyright:

  years: 2019, 2026

lastupdated: "2026-05-06"

keywords: migrated permissions, SoftLayer account permissions, migrated permission access group, migrated classic infrastructure permissions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Managing migrated SoftLayer account permissions
{: #migrated_permissions}

You can use migrated permission access groups to manage a set of classic infrastructure (SoftLayer) permissions for managing billing information and working with support cases. Access groups contain a set of users and service IDs that have the same access. The users in your SoftLayer account who were previously assigned account and support permissions are now assigned to the respective migrated permission access group. As a result, the permissions can be directly managed by using IAM access groups.
{: shortdesc}

These special access groups include all of the appropriate IAM policies to preserve the original behavior of the SoftLayer account permissions. For example, for a user to continue to view all updates from all users on a support case, the migrated permission access groups for the ticketing SoftLayer account permissions include an additional IAM policy on the User Management service with the viewer role assigned. For more information, see [Assigning user access for working with support cases](/docs/iam?topic=iam-account-services#support-center-account-management).

After your classic infrastructure permissions are migrated, you must discontinue use of those permissions and stop using the SoftLayer CLI or API to manage them. See the following table for the migrated classic infrastructure permissions that are now a part of IAM access groups. Access groups are created only for the permissions that are already assigned to users, so you might notice a subset of the access groups that are in your account that is listed in the following table.
{: note}

You can continue to manage these migrated classic infrastructure permissions for users directly through IAM by adding and removing users from the access groups. The access group policies are locked to preserve the access behavior for their members. However, you might find it helpful to create new access groups that include a combination of access policies for the [account management services](/docs/iam?topic=iam-account-services). The following table outlines the details of an IAM access policy that includes the permission from the migrated permission access group so that you can re-create and even combine these permissions with others in a new access group.

| Migrated Permission Access Group Name | Description                                                                                    | Account Management Service         | IAM Role       |
|---------------------------------------|------------------------------------------------------------------------------------------------|------------------------------------|----------------|
| View account summary                  | View the account summary page and invoices and payments.                                       | Billing                            | Viewer         |
| Get compliance reports                | Request compliance reports.                                                                    | Billing                            | Viewer         |
| Edit company profile                  | Edit the company profile information.                                                          | Billing                            | Editor         |
| Update payment details                | Update the recurring monthly payment information.                                              | Billing                            | Editor         |
| Limit EU case restriction             | Enable or disable the EU Supported option to restrict support case data to the European Union. | Billing                            | Not applicable |
| Add cases and view orders             | Create support cases and view all orders.                                                      | Support Center                     | Editor         |
| Edit cases                            | Edit any support case.                                                                         | Support Center                     | Editor         |
| Search cases                          | Search all support cases if the view cases permission is also assigned.                        | Support Center                     | Viewer         |
| View cases                            | View all support cases.                                                                        | Support Center and User Management | Viewer, Viewer |
{: caption="Migrated infrastructure permissions that are mapped to IAM roles" caption-side="top"}

For the view cases access, create two separate policies with the viewer role for the Support Center and User Management services. The policy on the User Management service helps ensure that the user views all cases in the account regardless of who opened them. Without the policy on the User Management service, if the account owner has restricted users' ability to view other users in the account, the user's view of cases might be limited to only the ones they opened themselves.
{: note}

## Assigning new IAM access policies for migrated permissions
{: #migrated-permissions-iam}

To re-create the migrated permissions that are available in each access group, you can assign policies to individual users or create new access groups in your account. The benefit of creating a new access group is that you can choose to combine a set of permissions for one access group rather than manage a set of access groups with a granular scope of access set for each. For this example, the steps explain how to create a new access group and assign an equivalent access policy for viewing the account summary and viewing all support cases.

Re-creating these permissions by assigning new IAM access policies for the account management services might include permissions in addition to the single permission that is available in the migrated permission access group. For example, if you assign a user the viewer role on the Billing service, that user can do more than view the account summary. For a full list of the actions that are allowed for each role, see [Assigning access to account management services](/docs/iam?topic=iam-account-services).
{: important}

To create an access group, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Access groups**.
2. Click **Create**.
3. Enter a name and an optional description for your group, and click **Create**.
4. Click **Add users**.
5. Select the users that you want to add from the list, and click **Add to group**. You can complete the same action from the **Service IDs** tab if you want to add any service IDs to the group.

After you set up your group with users and service IDs, assign access to the group. Remember, any policy that you set for the group applies to all members of the group.

1. Click the **Access** tab.
2. Click **Assign access**.
3. From the services, select **Billing** and click **Next**.
4. Select the **Viewer** role and click **Review**.
5. Click **Add**.
6. To assign a second access policy for the ability to view support cases, select the **Support Center** service.
7. Select the **Viewer** role and click **Review**.
8. Click **Add**.
9. To assign a third access policy for the ability to view all support cases regardless of how the account owner has set the account user visibility setting, select the **User Management** service.
10. Select the **Viewer** role and click **Review**.
11. Click **Add** to add your policy configuration to your policy summary.
12. Click **Assign**.

Three policies are now assigned to your group:

* A policy for viewing the account summary and all other actions that are associated with the viewer role in the Billing service.
* A policy for viewing and searching support cases in the account.
* A policy for viewing all users in the account and all other actions that are associated with the viewer role on the User Management service.
