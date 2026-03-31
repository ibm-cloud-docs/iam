---

copyright:

  years: 2015, 2026
lastupdated: "2026-03-31"

keywords: federated ID, password, enterprise SSO, single sign-on ID, API key login, one-time passcode login, temporary credential, to login, logging in, trusted profiles

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Logging in with a federated ID
{: #federated_id}

As a federated user that uses a corporate or enterprise single sign-on ID, you can log in to {{site.data.keyword.Bluemix}} from the console by using a federated ID and password. You can also log in from the command-line interface (CLI) by using a one-time passcode or an API key.
{: shortdesc}

By using federated IDs, you don't need to set up new login credentials specific to {{site.data.keyword.cloud_notm}}, for example, by using IBMid. Instead, users in your organization can easily log in to {{site.data.keyword.cloud_notm}} with their organization credentials through your identity provider (IdP).

When a user logs in, the user gets an IAM token, which is a temporary credential that expires after 1 hour. After that time, the token must be refreshed to secure the connection and to continue accessing account resources to which they are assigned access. For more information about using federated IDs, see [Setting up your {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-account-getting-started). For more information about using federated IDs, see [Enabling authentication from an external identity provider](/docs/iam?topic=iam-ibm-idp-integration).

Google login isn't available for users with federated IDs. For more information, see [known issues and limitations](/docs/account?topic=account-known-issues&interface=ui).
{: note}

## Using the console to log in
{: #login_console}
{: ui}

Use the following steps to log in to the {{site.data.keyword.cloud_notm}} console:

1. Go to the [{{site.data.keyword.cloud_notm}} login page](/login).
2. Enter your ID, and click **Continue**.
3. Enter your password.

After you log in, you are directed to the {{site.data.keyword.cloud_notm}} dashboard, which provides various development, account management, and infrastructure widgets.

## Using trusted profiles to log in to the console
{: #login_console_trustedprofile}
{: ui}

Account administrators use trusted profiles to manage specific access for account users. Each profile includes a different set of access policies that map to the roles or actions that you need to be productive. For example, a developer might use access group membership to do their daily work, but at some point during the week they might need to do some operations work in production environments. In this case, the developer would authenticate themselves and then take explicit action to apply a trusted profile that has the access policies they need to do operations work in production.

### Applying trusted profiles as an IBMid user
{: #login-ibmid-users}

If you are an IBMid user, complete the following steps to log in to the {{site.data.keyword.cloud_notm}} console by using a trusted profile:

1. Go to the [{{site.data.keyword.cloud_notm}} login page](/login).
2. Enter your IBMid, or if you are using single sign-on (SSO), enter your company email address, and click **Continue**.
3. Enter your password.
4. In the {{site.data.keyword.cloud_notm}} console, go to the account switcher and select the trusted profile that your account administrator created for you.

### Applying trusted profiles as an {{site.data.keyword.appid_short}} user
{: #login-appid-users}

If you are an {{site.data.keyword.appid_short}} user, complete the following steps to log in to the {{site.data.keyword.cloud_notm}} console by using a trusted profile:

1. Go to the `<DefaultIdPURL>` for your organization.

    If you don't know the `<DefaultIdPURL>`, ask your administrator. They have access to it from the Identity provider page. For more information, see [Logging in with external identity provider credentials](/docs/iam?topic=iam-ibm-idp-integration#log-in-external-idp)
    {: tip}

2. Enter your credentials and log in.
3. In the {{site.data.keyword.cloud_notm}} console, go to the account switcher and select the trusted profile that your account administrator created for you.<idp>

### Applying trusted profiles as a user federated with {{site.data.keyword.cloud_notm}} SAML
{: #login-federated-saml}

If you are a user federated with {{site.data.keyword.cloud_notm}} SAML, complete the following steps to log in to the {{site.data.keyword.cloud_notm}} console by using a trusted profile:

1. Go to the `<DefaultIdPURL>` for your organization.

    If you don't know the `<DefaultIdPURL>`, ask your administrator. They have access to it from the Identity provider page. For more information, see [Logging in with external identity provider credentials](/docs/iam?topic=iam-ibm-idp-integration#log-in-external-idp)
    {: tip}

2. Enter your credentials and log in.
3. In the {{site.data.keyword.cloud_notm}} console, go to the account switcher and select the trusted profile that your account administrator created for you.</idp>

## Using the CLI to log in
{: #usingthecli_login}
{: cli}

You choose to use either a one-time passcode or an API key to log in by using the CLI. You can find details based on whether you're using the {{site.data.keyword.cloud_notm}} or Red Hat OpenShift CLI in the following sections.


### Using a one-time passcode to log in with the CLI
{: #onetime_passcode}

When you use the one-time passcode option to log in with a federated ID, you specify the single-sign-on (SSO) parameter to get a one-time passcode, which you then enter at login.

Because a one-time passcode retrieves code from the {{site.data.keyword.cloud_notm}} console, it causes the use of a federated ID in your automation script to fail. Avoid trouble by using the API key option with an automated script.
{: tip}

#### From the {{site.data.keyword.cloud_notm}} CLI
{: #login_cli}

You can use two different methods to log in with the CLI. For the first method, use the following steps:

1. Specify the `--sso` option with the `ibmcloud login` command.
2. Follow the URL in the prompt to get the one-time passcode.
3. Copy and paste the passcode value in the CLI as your input.

   ```bash
   ibmcloud login --sso
   API endpoint: https://cloud.ibm.com

   Get One Time Code from https://identity-2.us-south.iam.cloud.ibm.com/identity/passcode to proceed.
   Open the URL in the default browser? [Y/n]>
   One Time Code >
   Authenticating...
   OK
   ```
   {: pre}

If you're already logged in to the console, you can use the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Log in to CLI and API**.
2. Copy the information for the {{site.data.keyword.cloud_notm}} CLI into the CLI.

#### From the Red Hat OpenShift CLI
{: #openshift_cli}

You can log in with a one-time passcode by using the following steps:

1. Log in to the console, and from the console, click the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Log in to CLI and API**.
2. Copy the information for the Red Hat OpenShift CLI and paste into the CLI.

### Using an API key in the CLI for authentication
{: #api_key}

The required API key is the {{site.data.keyword.cloud_notm}} API key that is used to authenticate with the {{site.data.keyword.cloud_notm}} platform, not the classic infrastructure API key, or {{site.data.keyword.cloud_notm}} service API key.

1. Create an API key with the [`ibmcloud iam api-key-create` command](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create). Use the `--file` option to generate an API key file instead of showing the key in the command window:

   ```bash
   ibmcloud iam api-key-create NAME [-d DESCRIPTION] [--file FILE]
   ```
   {: pre}

2. Log in with the API key. You can use the API key with the {{site.data.keyword.cloud_notm}} CLI in any of the following ways:

   * Call the API key directly:

      ```bash
      ibmcloud login --apikey <api_key_string>

      ```
      {: pre}

   * Call the API key with the key file:

      ```bash
      ibmcloud login --apikey @key_file_name
      ```
      {: pre}

   * Set an environment variable. Also, you can also set an environment variable on your system. For example, IBMCLOUD_API_KEY=api_key_string, where `api_key_string` is the custom value of the API key. After the environment variable is set, you can simply specify `ibmcloud login` from the CLI.

For Windows 10 PowerShell, you want to use `'@key_file_name'` with single quotation marks around the key file name.
{: tip}

## Using an API key to get an IAM token for authentication
{: #using_apikey}
{: api}

You can use an API key to get an IAM token to access your {{site.data.keyword.cloud_notm}} services. For example, you can run the following curl command to use an API key that is named `MY_APIKEY` to get an IAM token:

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/identity/token' -H 'Content-Type: application/x-www-form-urlencoded' -d
   'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=MY_APIKEY'
   ```
   {: pre}

For more information, see [Creating an IAM access token for a user or service ID by using an API key](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey).
