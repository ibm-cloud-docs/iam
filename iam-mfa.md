---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: MFA, multifactor authentication, IBMid MFA, two-factor authentication, account MFA, time-based one-time passcode, TOTP, security key

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Enabling MFA in your account
{: #enablemfa}

As an administrator on the IAM Identity Service or All IAM Account Management services, you can choose to require multifactor authentication (MFA) for every user in the account, just users with IBMids who do not use single sign-on (SSO), or individual users.
{: shortdesc}

Starting 3 May 2023, by default CLI logins with only a username and password are disabled for all users that have MFA set to **None**. This applies to users in new and existing accounts. Administrators can opt-out before that date in the {{site.data.keyword.cloud_notm}} console. For more information, see [Disabling CLI logins with only a password](/docs/account?topic=account-enablemfa#disabling-cli)
{: important}

View the MFA requirement for each user in your account to determine if they fulfill the requirement by generating an MFA status report. For more information, see [Identifying a user's MFA status](/docs/account?topic=account-id-user-mfa).

## Before you begin
{: #considerations}

The following information is helpful to consider before you enable MFA for your account to ensure that you know how it affects all users in your account:

* Enabling MFA for all users in your account affects all members of the account. If users in your account are members of multiple {{site.data.keyword.cloud_notm}} accounts, they must enroll for MFA at their next login even if they don't intend to use resources in the account where MFA is enabled.
* API keys for users and service IDs continue to work after MFA is enabled.
* MFA for your account applies to a user's login, but does not apply to API calls. If a user has permission to make API calls to resources in your account, the user can do so without completing MFA. If the user belongs to other accounts, the user can make API calls to resources in your account by using an API key from an account that did not require MFA.
* Plan a communication and support strategy for users in your account:
   * Choose a date and time that you plan to enable MFA that results in the least impact to your business.
   * Notify the users in your account after you enable MFA with information on how to get set up.

When you set the account default MFA, all IBMid users in your account are prompted for IBMid MFA authentication upon login. If you have other MFA factors set up for any IBMid users in your account, they are no longer prompted for those MFA factors. For example, if you previously enabled security questions in the customer portal for your classic infrastructure resources, the MFA account setting overrides the security questions option.
{: tip}

You can also enable and disable MFA in your account on the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page by clicking **Show accounts** > **Manage your own account**.
{: note}

## Enabling MFA
{: #enabling}
{: help}
{: support}

Enabling MFA does not affect users that are already logged in because MFA takes effect only at the time of login. Make sure that you notify your account users that MFA is enabled, and describe the impact to users at their next login.

The first time that you log in to your account after MFA settings are updated, you need to verify your identity by using two different verification methods. Methods for verification include email, text, or phone call, and you can use any combination of those options to verify your identity. After you verify your identity, you set up your authentication factors. If you need to update your verification methods or authentication factors later, see [Managing verification methods and MFA factors](/docs/account?topic=account-verification-authentication).
{: note}

### Enabling MFA for an account
{: #enabling-account}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Settings**.
1. Click **Authentication**.
1. Select the type of MFA that you want to enable in your account. For more information about the MFA options, see [MFA options](/docs/account?topic=account-types#mfa-options).

### Enabling MFA for an individual user
{: #enabling-user}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Users** and select the user whose MFA you want to update.
1. Go to the **MFA** section and click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit").
1. Select the type of MFA to enable for the user.

   By default, **Use account default** is selected. The account default is the MFA option that is enabled at the account level. To view the account default, go to **Manage > Access (IAM) > Settings > Authentication**.
   {: note}

1. Click **Save**.

You can view a list of users in your account that have an MFA requirement that is different from the account's default by going to **Manage > Access (IAM) > Settings > Authentication**. Then, view the **User-specific MFA** section.
{: tip}

## Disabling MFA
{: #disablemfa}

Disabling MFA does not affect users that are already logged in. The action impacts all new logins.

### Disabling MFA for an account
{: #disable-account}

1. Go to **Manage** > **Access (IAM)** > **Settings** > **Authentication** in the {{site.data.keyword.cloud_notm}} console.
1. Select **None**.

### Disabling MFA for an individual user
{: #disabling-user}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Users** and select the user whose MFA you want to update.
1. Go to the **MFA** section and click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit").
1. Select **None**.
1. Click **Save**.

### Disabling CLI logins with only a password
{: #disabling-cli}

[New]{: tag-new}

Increase the level of security for users that aren't required to complete multifactor authentication by disabling CLI logins with only a password for a user or the account. This way, you require an API key to log in to the CLI, or users can log in with `--sso`, without requiring your users to complete MFA on each login.

To disable CLI logins with only a password, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**
   - To apply this to an individual user, click **Users** and select the user whose MFA you want to update.
      1. Go to the **MFA** section and click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit").
   - To apply this to the account, click **Settings** > **Authentication**.
1. Select **None**.
1. Select **Disable CLI logins with only a password**
1. Click **Save** for an individual user.

Users are prompted only once for an additional factor if IBMid detects that a user is logging in to a new device or browser. Once a user logs in using an additional factor on a new device, they aren't prompted for that factor again. This prevents certain programmatic attack vectors and enhances the security of users’ accounts without prompting users each time they log in.
{: note}

{{/iam-ver-auth.md#resetting-mfa-factors}}

For more information, see [Why can't I log in with my MFA factors?](/docs/account?topic=account-troubleshoot-MFA).
