---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-31"

keywords: troubleshoot invite users, access to invite users, access to add users

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I get access to invite users to the account?
{: #troubleshoot-invite}
{: troubleshoot}

You must have specific access to invite users to an {{site.data.keyword.Bluemix}} account if you aren't the account owner. Without the correct access, you can't invite users to an account.
{: shortdesc}

When you click **Invite users**, the following message might be displayed:
{: tsSymptoms}

```text
Looks like you don't have access to invite users. You must be assigned the editor or administrator role for the User management service. Contact your account owner for access.
```

You aren't assigned the correct access.
{: tsCauses}

To invite users and manage outstanding invitations, you must be an account owner, an organization manager, a user with an IAM access policy with the Editor role or higher on the user management account management service, or you must have classic infrastructure permissions to add users.
{: tsResolve}

To review your assigned access in the account, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Users**.
2. Select your name.
3. Review the assigned access in the **Access** tab.

If you aren't assigned the correct access, contact the account owner. After you have the correct access, go to **Manage > Access (IAM)**, then select **Users**, and click **Invite users** to add users to the account.

If you're the account owner and can't invite users, contact [Support](/unifiedsupport/supportcenter){: external}.
