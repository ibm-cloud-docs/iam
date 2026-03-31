---

copyright:
  years: 2020, 2026
lastupdated: "2026-03-31"

keywords: troubleshoot migrated softlayer permissions, migrated billing permission, migrated support permission

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I manage migrated billing and support case permissions in {{site.data.keyword.cloud_notm}}?
{: #troubleshoot-migrated-permissions}
{: troubleshoot}

A set of SoftLayer billing and support permissions are now available as migrated permission access groups in {{site.data.keyword.Bluemix}}.
{: shortdesc}

With the initial migration of users and permissions for managing billing and support cases from your SoftLayer account to your linked {{site.data.keyword.cloud_notm}} account, some users might not have these permissions. However, all migrated permission access groups are now assigned the correct IAM access policies, ensuring that all users are assigned the correct access that they had previously.

Users don't seem to have the same managing billing and support case permissions in the {{site.data.keyword.cloud_notm}} console that they were previously assigned in your SoftLayer account.
{: tsSymptoms}

Your migrated permissions access groups might not be assigned the correct access policies when the users were initially migrated.
{: tsCauses}

As of 20 May 2019, all [migrated permission access groups](/docs/iam?topic=iam-migrated_permissions) have the correct policies that are assigned for managing billing information and support cases. If you tried to use these groups before this date, the access groups that are missing equivalent IAM access policies might have caused a mismatch in the assigned access between the SoftLayer permissions and IAM access. This is resolved. You can go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and then select **Access groups** to review the users and policies that are assigned to each access group.
{: tsResolve}
