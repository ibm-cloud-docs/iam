---

copyright:
  years: 2020, 2026
lastupdated: "2026-03-31"

keywords: restrict api keys, block users from creating api keys, restrict api key creation

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Restricting users from creating API keys
{: #allow-api-create}

By default, all members of an account can create {{site.data.keyword.cloud}} API keys. However, that access can be restricted so that only members with the correct access can create these user API keys by using the API key creation setting.
{: shortdesc}

Restricting the ability to create API keys makes sense if you want users in your account to always log in interactively, meaning you don't want automation scripts to run that can log in users automatically by using an API key. For more information about API keys, see [Managing user API keys](/docs/iam?topic=iam-userapikey).

If API key creation is [enterprise-managed]{: tag-cyan}, the setting defined at the account-level applies if the enterprise-managed setting is less strict or removed.

## Restricting API key creation in the console
{: #allow-all-api-create}
{: ui}

To turn on the setting to restrict users from creating user API keys, you must have the following assigned access:

* An IAM policy with the `Administrator`, `Operator`, or `Editor` role on the [IAM Identity Service](/docs/iam?topic=iam-account-services#identity-service-account-management).

If you turn on the Restrict API key creation setting, users in your account require specific access to create API keys, including the account owner. To restrict who can create API keys, use the following steps:

Enabling this setting affects only the creation of user API keys. It does not affect API keys for service IDs.
{: note}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Settings**.
1. In the Account section, enable the **Restrict API key creation** setting.
1. Click **Yes** to confirm.

Now that the setting is enabled to restrict users from creating API keys, you can assign the required access to enable specific users to continue creating user API keys. Remember, the account owner is also required to be assigned this explicit access.
{: important}

## Restricting API key creation by using Terraform
{: #allow-all-api-create-terraform}
{: terraform}

If you turn on the API key creation setting, users in your account require specific access to create API keys, including the account owner.

To turn on the setting to restrict users from creating user API keys, you must have the following assigned access:

- An IAM policy with the `Administrator`, `Operator`, or `Editor` role on the [IAM Identity Service](/docs/iam?topic=iam-account-services#identity-service-account-management).

Before you can set limits for login sessions by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

To restrict who can create API keys, use the following steps:

Enabling this setting affects only the creation of user API keys. It does not affect API keys for service IDs.
{: note}

1. Create an argument in your `main.tf` file. The following example enables the API key creation setting by using the `ibm_iam_account_settings` and `iam_account_settings_instance` resources.
1. Defines whether or not creating platform API keys is access controlled. Supported valid values are:
   * RESTRICTED - to apply access control
   * NOT_RESTRICTED - to remove access control
   * NOT_SET - to unset a previous set value.

   ```terraform
   resource "ibm_iam_account_settings" "iam_account_settings_instance" {
   restrict_create_platform_apikey  = "RESTRICTED"
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

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings#restrict_create_platform_apikey).

Now that the setting is enabled to restrict users from creating API keys, you can assign the required access to enable specific users to continue creating user API keys. Remember, the account owner is also required to be assigned this explicit access.
{: important}

## Assigning access to create API keys with restrictions enabled
{: #restrict-api-create-access}
{: ui}

If the API key creation setting is enabled, only users, including the account owner, assigned the `User API key creator` role on the IAM Identity Service can create API keys.

The quickest way to assign a group of users the required access for creating API keys is to create an access group and assign the group the required role. For more information about assigning access policies, see [Setting up access groups](/docs/iam?topic=iam-groups).
{: tip}
