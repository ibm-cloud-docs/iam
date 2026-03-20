---

copyright:

  years: 2023, 2026
lastupdated: "2026-03-20"

keywords: MFA, MFA status, fulfill MFA, multifactor authentication, MFA requirement, MFA report

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Identifying a user's MFA status
{: #id-user-mfa}

The first time that users log in to your account after you [enable multifactor authentication (MFA)](/docs/account?topic=account-enablemfa), they must set up their authentication factors. Otherwise, your account is subject to security vulnerabilities and attacks. You can identify the users in your account who don't meet your MFA requirements by generating an MFA status report.
{: shortdesc}

You must have the Administrator role on the IAM Identity Service to view and update the report. The following actions are included in this role.

- The action `iam-identity.mfa-status.get` is required to view the report.
- The action `iam-identity.report.create` is required to generate a new report.

## Viewing the MFA status of users in the console
{: #view-user-mfa-status}

To view the MFA status of users in the console, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **MFA status**.
2. Click **Update report** to view the most recent report in your account. 

   Only the most recent report is available. When you generate a new report, any reports older than a day are deleted.
   {: note}

3. Contact the users in your account who don't satisfy the MFA requirements. Ask them to comply by logging in and setting up factors. For more information, see [Managing your authentication factors](/docs/account?topic=account-verification-authentication#auth-factors).
