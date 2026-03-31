---

copyright:

  years: 2023, 2026
lastupdated: "2026-03-31"

keywords:

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to {{site.data.keyword.cloud_notm}} MFA
{: #migrate-mfa}

The deprecated legacy account-based multifactor authentication (MFA) was available to accounts with classic infrastructure before the release of the {{site.data.keyword.cloud_notm}} MFA. Nonclassic resources are not secured by this legacy offering. You must migrate to the {{site.data.keyword.cloud_notm}} MFA to secure the full range of {{site.data.keyword.cloud_notm}} offerings.
{: shortdesc}

You must have access to manage your own login settings for the account. Otherwise, you'll need to contact the account admin to disable the settings.

To migrate to the {{site.data.keyword.cloud_notm}} MFA:

1. Set up {{site.data.keyword.cloud_notm}} MFA. You must have at least the role of administrator for the IAM (Identity and Access Management) service. For more information, see [Enabling MFA](/docs/iam?topic=iam-enablemfa#enabling).
2. Disable the legacy account-based MFA.

   1. Go to **Manage** > **Access (IAM)** > **Users** > select your name > **User details**.
   1. Find the **Legacy account-based MFA** section and toggle off the **User one-time passcode authentication** option.
   1. Then, click **Set up**.
   1. Click **Remove** so that all existing setup for legacy account-based MFA is deleted for this user.

These steps must be completed by each user in the account to migrate to the {{site.data.keyword.cloud_notm}} MFA.
{: important}
