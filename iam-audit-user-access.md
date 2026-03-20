---

copyright:

  years: 2022, 2026
lastupdated: "2026-03-20"

keywords: audit, audit user access, user access, auditor role

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Auditing user access policies
{: #audit-user-access}

If you are the account owner or have the Editor role or higher on the user management account management service, you can export an access policiy report for each user in your account. The access policy report lists all of the access policies that the user is assigned to as well as the access policies of the access groups that the user is a memeber of.
{: shortdesc}

Auditing user's access policies ensures that you're using the principle of least privilege. The best practice for assigning access is to give the least amount of access that is required. Use the report to determine if the user is assigned to the appropriate access policies, and take the needed action to reduce the number of access policies and inflated access across the account.


## Exporting a report
{: #export-report-user-access}

To export the report, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access(IAM)**, and select **Users**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg) > **Access report** for the user that you want to audit.
1. Click **Download JSON** or **Download CSV**.


