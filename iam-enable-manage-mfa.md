---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-23"

keywords: MFA, multifactor authentication, IBMid MFA, two-factor authentication, account MFA, time-based one-time passcode, TOTP, security key, security key, MFA requirement, MFA report

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Enabling and managing verification methods and MFA
{: #enablemfa}

As an administrator on the IAM Identity Service or All IAM Account Management services, you can choose to require multifactor authentication (MFA) for every user in the account, just users with IBMids who do not use single sign-on (SSO), or individual users.
{: shortdesc}

Starting 3 May 2023, by default CLI logins with only a username and password are disabled for all users that have MFA set to **None**. This applies to users in new and existing accounts. Administrators can opt-out before that date in the {{site.data.keyword.cloud_notm}} console. For more information, see [Disabling CLI logins with only a password](/docs/iam?topic=iam-enablemfa#disabling-cli).
{: important}

View the MFA requirement for each user in your account to determine if they fulfill the requirement by generating an MFA status report. For more information, see [Identifying a user's MFA status](/docs/iam?topic=iam-enablemfa#id-user-mfa).

If MFA is [enterprise-managed]{: tag-cyan}, the MFA defined at the account-level applies if the enterprise-managed setting is less strict or removed.

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

The first time that you log in to your account after MFA settings are updated, you need to verify your identity by using two different verification methods. Methods for verification include email, text, or phone call, and you can use any combination of those options to verify your identity. After you verify your identity, you set up your authentication factors. If you need to update your verification methods or authentication factors later, see [Managing verification methods and MFA factors](/docs/iam?topic=iam-verification-authentication).
{: note}

### Enabling MFA for an account
{: #enabling-account}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Settings**.
1. Click **Authentication**.
1. Select the type of MFA that you want to enable in your account. For more information about the MFA options, see [MFA options](/docs/iam?topic=iam-types#mfa-options).

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

For more information, see [Why can't I log in with my MFA factors?](/docs/iam?topic=iam-troubleshoot-MFA).

## Identifying a user's MFA status
{: #id-user-mfa}

The first time that users log in to your account after you enable MFA, they must set up their authentication factors. Otherwise, your account is subject to security vulnerabilities and attacks. You can identify the users in your account who don't meet your MFA requirements by generating an MFA status report.

You must have the Administrator role on the IAM Identity Service to view and update the report. The following actions are included in this role.
- The action `iam-identity.mfa-status.get` is required to view the report.
- The action `iam-identity.report.create` is required to generate a new report.

### Viewing the MFA status of users in the console
{: #view-user-mfa-status}

To view the MFA status of users in the console, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **MFA status**.
2. Click **Update report** to view the most recent report in your account.

   Only the most recent report is available. When you generate a new report, any reports older than a day are deleted.
   {: note}
3. Contact the users in your account who don't satisfy the MFA requirements. Ask them to comply by logging in and setting up factors. For more information, see [Managing your authentication factors](/docs/iam?topic=iam-enablemfa#auth-factors).

## Managing verification methods and MFA factors
{: #verification-authentication}

You can add and delete your verification methods and authentication factors on the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page. You might want to update these settings if an email address or phone number that you use to verify your identity or authenticate to {{site.data.keyword.Bluemix}} changes or becomes inaccessible.

You can view a log of recent changes to your verification methods and authentication factors by clicking **Show events** on the Verification methods and authentication factors page.
{: tip}

### Accessing your verification methods and authentication factors
{: #ver-auth-login}

Verification methods and authentication factors add an extra layer of security to accounts. To view and modify your verification methods and authentication factors, complete the following steps:

1. Go to the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page.
1. Validate your identity with two different verification methods.
   You must verify your identity each time that you access the Verification methods and authentication factors page.
   {: note}

1. Enter the one-time password (OTP) that is sent to the method you choose, and click **Verify**. Complete this step for each method.

### Managing methods for verifying your identity
{: #verificaiton-methods}

You can add and remove the verification methods that identify you as a user in the account. Make sure that you add backup verification methods in case one of them becomes inaccessible. Verification methods are used each time that you access the Verification methods and authentication factors page. If a verification method is not in use, remove it.

If one or more verification methods are inaccessible, and you are unable to verify your identity, you can open a [support case](/unifiedsupport/supportcenter) to reset these methods.

#### Adding a verification method
{: #add-verificaiton}

To add a verification method, complete the following steps:

1. From the Verification methods and authentication factors page, click **Manage verification methods**.
1. Click **Add**.
1. Select a new verification method.
1. Name the verification method.
1. Enter the phone number or email address.
1. Click **Send OTP**.
1. Enter the OTP that you receive.
1. Click **Complete**.

#### Removing a verification method
{: #remove-verificaiton}

To remove a verification method, complete the following steps:

1. From the Verification methods and authentication factors page, click **Manage verification methods**.
1. Select the method that you want to remove.
1. Click **Remove**.
1. Click **Yes** to confirm that you want to remove the verification method.

### Managing your authentication factors
{: #auth-factors}

If an account administrator enables MFA in at least one of the accounts that you are a member of, you must use an authentication factor, in addition to your username and password, to securely log in to {{site.data.keyword.cloud_notm}}.

#### Adding authentication factors
{: #add-auth-factors}

Authentication factors are used to authenticate yourself each time you log in to {{site.data.keyword.cloud_notm}} if an administrator enables MFA in at least one of the accounts you are a member of. These factors can be something that you have, like a security key, or that you receive, like a time-based one time passcode (TOTP), or OTP. Make sure you add backup authentication factors. This way, you can prevent losing access to {{site.data.keyword.cloud_notm}} in the case that one of them becomes inaccessible.

1. From the Verification methods and authentication factors page, click **Show authentication factors**.
1. Click **Add**.
1. Select an authentication factor and enter a name. This name is used to identify the authentication factor.
    1. For **Security key**, insert your security stick, and click **Register Key**.
    1. For **TOTP**, scan the QR code, and enter the code that is generated by your authenticator app.
    1. For **Email-based**, enter the email address where you want to receive the OTPs.
       1. Click **Send OTP**.
       1. Enter the OTP that you receive.
1. Click **Complete**.

#### Removing authentication factors
{: #remove-auth-factors}

Remove an authentication factor if you don't have access to it anymore to ensure the security of your account.

1. From the Verification methods and authentication factors page, click **Show authentication factors**
1. Select an authentication factor.
1. Click **Remove**.
1. Click **Yes** to confirm that you want to remove the authentication factors.

You can also enable and disable MFA for your own account on the Verification methods and authentication factors page. Changing the authentication settings for an account impacts all members of the account. By enabling MFA, you can require more secure logins for your account. For more information, see [Enabling MFA in your account](/docs/iam?topic=iam-enablemfa).
{: tip}

#### Resetting authentication factors
{: #resetting-mfa-factors}

You can update or reset your authentication methods if the email address or phone number that you use to authenticate to the {{site.data.keyword.cloud_notm}} console changes or becomes inaccessible.

1. Go to the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page.
2. Validate your identity with two different verification methods.
3. Click **Show accounts**.
4. Take note of the Authentication setting for each account.
   1. If the account uses MFA for **IBMid users**, work with the [IBMid help desk](https://www.ibm.com/docs/en/ibmid){: external} to reset your authentication factors.
   1. If the account uses MFA for **All users**, you can reset your authentication factors on the Verification methods and authentication factors page.
      1. Click the checkbox next to the MFA method that you want to reset and click Remove.
      1. Set up your new MFA factor the next time that you login to {{site.data.keyword.cloud}}.
