---

copyright:

  years: 2022, 2026
lastupdated: "2026-03-31"

keywords: inactive identity, inactive identities, inactive, inactive users, inactive service IDs, inactive trusted profiles, inactive API keys

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Identifying inactive identities
{: #id-inactive-identities}

Identities are considered inactive when they aren't logged in or used in 30 days. You can review which users, service IDs, trusted profiles, and API keys in your account are inactive. You might want to remove inactive identities if they are no longer needed. Removing access for inactive identities can reduce the risk of unauthorized access to your {{site.data.keyword.cloud_notm}} resources and help you manage access more efficiently.
{: shortdesc}

To manage inactive identities, you must be assigned the Administrator role on the IAM Identity Service.

When you delete an identity from the table, for example a user, and click **Update report**, it takes a few minutes for a new report to exclude the deleted user.
{: note}

## Managing inactive identities in the console
{: #manage-inactive-identities}

To view inactive identities in the console, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Inactive identities**.
1. Click **Update report** to view the most recent report of the inactive identities in your account.

   Only the most recent report is available. Reports older than a day are deleted when generating a new report.
   {: note}

1. Select a tab to review a list of inactive identities.
1. To delete inactive identities that are no longer in use, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Remove**.

Before you delete an identity, confirm that they are inactive for at least 30 days.
{: note}

To learn more about the implications of removing or deleting identities in your account, review the following documentation:

   - [Removing users from an account](/docs/iam?topic=iam-iamuserinv&interface=ui#remove-user-acount-ui)
   - [Deleting service IDs by using the console](/docs/iam?topic=iam-serviceids&interface=ui#delete-group-ui)
   - [Removing trusted profiles](/docs/iam?topic=iam-trusted-profile-update&interface=ui#remove-tp-console)
   - [Deleting an API key](/docs/iam?topic=iam-userapikey&interface=ui#delete_user_key)
   - [Deleting an API key for a service ID](/docs/iam?topic=iam-serviceidapikeys&interface=ui#delete_service_key)
