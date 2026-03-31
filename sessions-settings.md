---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-31"

keywords: user session, inactivity, sign out, concurrent, login session, trusted profiles

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Setting limits for login sessions
{: #iam-work-sessions}

Improve the security of your account by requiring account users to enter their login credentials at customized intervals. As an account owner or user assigned the administrator role for the Identity service, you can select the time that a user's active session can last before they need to enter their credentials again. You can also choose the duration that a user is inactive before they are signed out of their session and are required to enter their credentials again.
{: shortdesc}

To review and end active sessions to help maintain the security of your account, see [Monitoring your login sessions](/docs/account?topic=account-monitor-your-session).
{: tip}

If limits for login sessions are [enterprise-managed]{: tag-cyan}, the setting defined at the account-level applies if the enterprise-managed setting is less strict or removed.

## Before you begin
{: #work-sessions-access}

If you have the following access, you can update the settings for login sessions:

* Account owners
* Editor or admin role on all account management services
* Editor or admin role on IAM identity service

If a user is a member of multiple accounts, the lowest value of each setting is applied to their session. For example, let's say a user is a member of two accounts: `dev account` and `test account`. If `dev account` has a 15 minute inactivity timeout, and `test account` has a 30 minute inactivity timeout, the 15 minute inactivity timeout is applied to both accounts.
{: note}

Before you can set limits for login sessions by using Terraform, make sure that you have completed the following:
{: terraform}

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.
{: terraform}

## Setting duration of active sessions
{: #sessions-active}
{: ui}

An active session is how long a user is continuously working in their account. How an active session is gauged also depends on the duration of your session sign out due to inactivity limit. For instance, if you set the sign out to 2 hours, then the user would need to interact with the account one time between those 2 hours.

To update your user's active sessions settings, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Settings**.
1. From the Login session section, click the **Edit** icon ![Edit icon](../icons/icon_write.svg "Edit") from the Active sessions tile.
1. Enter the time limit. The longest a session can last is 720 hours.
1. Click **Save**.

## Setting duration of active sessions by using Terraform
{: #sessions-active-terraform}
{: terraform}

An active session is how long a user is continuously working in their account. How an active session is gauged also depends on the duration of your session sign out due to inactivity limit. For instance, if you set the sign out to 2 hours, then the user would need to interact with the account one time between those 2 hours.

To update your user's active sessions settings by using terraform, complete the following steps:

1. Create an argument in your `main.tf` file. The following example sets the duration of an active session by using the `ibm_iam_account_settings` and `iam_account_settings_instance` resources.
1. Enter the period of time in seconds in which you want a session to invalidate due to inactivity. Supported valid values are
   * Any whole number between between 900 and 7200.
   * Use `NOT_SET` to unset account setting and use service default.

   ```terraform
   resource "ibm_iam_account_settings" "iam_account_settings_instance" {
   session_invalidation_in_seconds = "7200"
   }
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings#allowed_ip_addresses).

### Setting session duration for trusted profiles
{: #sessions-active-tp}
{: ui}

For more information, see [Updating trusted profiles](/docs/iam?topic=iam-trusted-profile-update&interface=ui#session-duration-tp).

## Setting the sign out due to inactivity duration
{: #sessions-inactivity}
{: ui}

An inactive session is when the user hasn't completed any requests that send a token for validation for the duration selected. If the sign out due to inactivity duration is 1 hour, then the user will be signed out after an hour if they haven't done anything in their account in that time. To update your user's sign out due to inactivity settings, complete the following steps.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Settings**.
1. From the Login session section, click the **Edit** icon ![Edit icon](../icons/icon_write.svg "Edit") from the Sign out due to inactivity tile.
1. Enter the time limit. The longest an inactive session can last is 24 hours.
1. Click **Save**.

## Setting the sign out due to inactivity duration by using Terraform
{: #sessions-concurrent-}
{: terraform}

An inactive session is when the user hasn't completed any requests that send a token for validation for the duration selected. If the sign out due to inactivity duration is 1 hour, then the user will be signed out after an hour if they haven't done anything in their account in that time. To update your user's sign out due to inactivity settings, complete the following steps.

To update your user's sign out due to inactivity duration by using terraform, complete the following steps:

1. Create an argument in your `main.tf` file. The following example sets the inactive sign out by using the `ibm_iam_account_settings` and `iam_account_settings_instance` resources.
1. Enter the period of time in seconds in which you want a session to invalidate due to inactivity. Supported valid values are
   * Any whole number between between 900 and 7200.
   * Use `NOT_SET` to unset account setting and use service default.

   ```terraform
   resource "ibm_iam_account_settings" "iam_account_settings_instance" {
     session_expiration_in_seconds = "3600"
   }
   ```
   {: codeblock}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings#allowed_ip_addresses).

## Setting the number of allowed concurrent sessions
{: #sessions-concurrent}
{: ui}

You can choose the maximum number of concurrent sessions that are allowed for your account users. Concurrent sessions are active sessions that the user is signed into at one time. Users can have multiple sessions open by using different browsers or several logins with the {{site.data.keyword.cloud_notm}} CLI. Multiple concurrent sessions are more beneficial for parallel workloads.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Settings**.
1. From the Concurrent sessions tile, click the **Edit** icon ![Edit icon](../icons/icon_write.svg "Edit"), click the Unlimited dropdown > **Limit sessions**.
1. Enter the limit. Users can have an unlimited number of concurrent sessions.
1. Click **Save**.

## Setting the number of allowed concurrent sessions by using Terraform
{: #sessions-concurrent-terraform}
{: terraform}

You can choose the maximum number of concurrent sessions that are allowed for your account users. Concurrent sessions are active sessions that the user is signed into at one time. Users can have multiple sessions open by using different browsers or several logins with the {{site.data.keyword.cloud_notm}} CLI. Multiple concurrent sessions are more beneficial for parallel workloads.

To update your user's allowed number of concurrent sessions by using terraform, complete the following steps:

1. Create an argument in your `main.tf` file. The following example sets the number of allowed concurrent sessions by using the `ibm_iam_account_settings` and `iam_account_settings_instance` resources.
2. Enter the period of time in seconds in which you want a session to invalidate due to inactivity. Supported valid values are
   * Any whole number greater than '0'.
   * Use `NOT_SET` to unset account setting and use service default.

   ```terraform
   resource "ibm_iam_account_settings" "iam_account_settings_instance" {
    max_sessions_per_identity = "3"
   }
   ```
   {: codeblock}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings#allowed_ip_addresses).

## Determining when sessions are created
{: #sessions-nonsessions-2}

Login session settings apply only when there is connected login session. If no login session is created, then [limits for IAM tokens](/docs/iam?topic=iam-token-limit) apply. Use the following table to help you understand when each setting applies.

Sessions are created when a user logs in to the {{site.data.keyword.cloud}} CLI or {{site.data.keyword.cloud}} console. For example, if you create a user API key and use it for the {{site.data.keyword.cloud}} CLI, this generates a login session. However, if you use the same API key to create a token for API calls, like [creating an IAM access token for a user or service ID](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey), this does not generate a session.

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| {{site.data.keyword.cloud}} CLI | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |                                                |                                                |
{: caption="Sessions and refresh token availability - Users" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the login type. The column headers identify whether sessions and refresh tokens are available. To understand session and refresh token availability for each login type, navigate to the row for the login type you're interested in. Use the buttons before the table to change the identity type."}
{: #table01}
{: tab-title="Users"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| {{site.data.keyword.cloud}} CLI | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |                                                |                                                |
{: caption="Sessions and refresh token availability - Trusted profiles for federated users" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the login type. The column headers identify whether sessions and refresh tokens are available. To understand session and refresh token availability for each login type, navigate to the row for the login type you're interested in. Use the buttons before the table to change the identity type."}
{: #table02}
{: tab-title="Trusted profiles - federated users"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | N/A | N/A |
| {{site.data.keyword.cloud}} CLI |         | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |         |                                                |
{: caption="Sessions and refresh token availability - Service IDs" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the login type. The column headers identify whether sessions and refresh tokens are available. To understand session and refresh token availability for each login type, navigate to the row for the login type you're interested in. Use the buttons before the table to change the identity type."}
{: #table03}
{: tab-title="Service IDs"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}
