---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: user list visibility, users page setting, user view access, limit access to users list, user list access, parent user, update parent

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Controlling user visibility
{: #iam-user-setting}

There are two ways to change how a user views other users in an account. The first is by using the user list visibility setting. And, the second is for classic infrastructure users, and it is directly related to the parent user that is listed. The assigned parent user determines which users a specific user can view when the setting for user list visibility is enabled.
{: shortdesc}

## Setting user view access
{: #userlistview}

As an {{site.data.keyword.Bluemix}} account owner, you can view all users in your account and define how users can view other users in the account. By using the user list visibility setting, you can control how users see others across the account.

When the setting is disabled, any user in the account can view other users from the Users page in {{site.data.keyword.cloud_notm}} console. When the setting is enabled, users can view only specific types of users in the account:

* Users invited by the user
* Users who are their descendants in the classic infrastructure user hierarchy, meaning the users that they invited or that one of their descendants invited.

By default, the setting is disabled for your account. To update this setting, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Settings**.
1. From the Account section, enable **Restrict user list visibility**.
1. Click **Yes** to confirm.

## Updating a user's parent user
{: #update-parent}

If you have the correct access, you can update the parent for a user. Updating the parent user affects how a user views other users in the account when the setting for user list visibility is enabled. Users can view only other users for which they are a parent and any other users who are invited by those descendants of the parent user.

If you have the following access, you can update the parent for another user:

* An IAM policy with Editor or higher role on the User management service.
* You are an ancestor in the classic infrastructure hierarchy for the user and you have the Manage user classic infrastructure permission assigned.

To update a user's parent, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Users**.
2. Select a user's name from the list.
3. From the User details page, select a new parent user from the **Parent** menu.
4. Click **Apply**.
