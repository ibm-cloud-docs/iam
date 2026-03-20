---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: specific IP addresses, IP addresses, restrict IP access, IP address access, allow IP access

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Allowing specific IP addresses
{: #ips}

By default, all IP addresses can be used to log in to the {{site.data.keyword.cloud}} console and access classic infrastructure APIs. You can specify which IP addresses have access and which IP addresses are restricted. You can specify this access at the user level or at the account level. Currently, only public IP addresses are supported.
{: shortdesc}

If IP addresses access is [enterprise-managed]{: tag-cyan}, you can restrict access to a subset of IPs within the enterprise-managed list.

## Before you begin
{: #before-allowing-ips}

* If an IP address restriction is defined for both the account and the user, the IP address needs to match both specifications to be able to generate an IAM token.
* When you allow only specific IP addresses to access an {{site.data.keyword.cloud_notm}} account, users can't access the {{site.data.keyword.cloud_notm}} Shell CLI. This is because the Cloud Shell is hosted on a shared platform that can't satisfy the IP address allowlist.

## Allowing specific IP addresses for a user
{: #ips_user}
{: ui}

If you are assigned to the following access, you can update the restricted IP addresses for another user:

* An IAM policy with the Editor or higher role on the User management service.
* You are an ancestor in the classic infrastructure hierarchy for the user and you have the Manage users classic infrastructure permission assigned

If you enable the User-managed login setting on your User details page, you can manage this setting for yourself.
{: tip}

To restrict a user to using only specific IP addresses, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Users**.
2. Select a user from the list.
3. From the User details page, go to the **IP address restrictions** section.
4. For **Cloud platform**, enter the IP addresses. The IP addresses listed are the only ones from which this user can log in to {{site.data.keyword.Bluemix}}.
5. For **Classic infrastructure**, enter the IP addresses. The IP addresses listed are the only ones from which the user can call a classic infrastructure API.

      You can enter a single IP address `17.5.7.8`, an IP address range `17.5.7.8 - 17.5.9.5`, or IP subnets `17.5.7.8.0/16`. Use IPv4 or IPv6 addresses, and separate multiple values with a comma.
      {: note}

6. Click **Save**.

To enter a classic infrastructure IP address, the user must have already created a classic infrastructure API key.
{: note}



## Allowing specific IP addresses for an account
{: #ips_account}
{: ui}

If you are assigned the following access, you can update the restricted IP addresses for an account:

* An IAM policy with the Editor, Operator, or Administrator role on the IAM identity service.

To restrict all users to using only specific IP addresses, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Settings**.
1. From the Account section, enable **Restrict IP address access**.
1. Enter the IP addresses. The IP addresses listed are the only ones from which users and service IDs using an API key in the account can log in to {{site.data.keyword.Bluemix}}.

   You can enter a single IP address `17.5.7.8`, an IP address range `17.5.7.8 - 17.5.9.5`, or IP subnets `17.5.7.8.0/16`, or a [network zone](/docs/iam?topic=iam-context-restrictions-whatis#network-zones-whatis) `networkZoneName`. Use IPv4 or IPv6 addresses, and separate multiple values with a comma.
   {: note}

1. Click **Save**.

## Allowing specific IP addresses for an account by using Terraform
{: #ips_account_terraform}
{: terraform}

If you are assigned the following access, you can update the restricted IP addresses for an account:

* An IAM policy with the Editor, Operator, or Administrator role on the IAM identity service.

To restrict all users to using only specific IP addresses, complete the following steps:

1. In your Terraform configuration file, find the Terraform code that you used to create the `iam_account_settings_instance`.
1. Enter the IP addresses that you want to restrict all users to using. The IP addresses listed are the only ones from which users and service IDs using an API key in the account can log in to {{site.data.keyword.Bluemix}}.

   ```terraform
    resource "ibm_iam_account_settings" "iam_account_settings_instance" {
      allowed_ip_addresses = "17.5.7.8, 17.5.7.8 - 17.5.9.5, 17.5.7.8.0/16"
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

You can enter a single IP address `17.5.7.8`, an IP address range `17.5.7.8 - 17.5.9.5`, or IP subnets `17.5.7.8.0/16`, or a [network zone](/docs/iam?topic=iam-context-restrictions-whatis#network-zones-whatis) `networkZoneName`. Use IPv4 or IPv6 addresses, and separate multiple values with a comma.
{: note}

## Unlocking an account
{: #unlock_account}

If a user cannot access the {{site.data.keyword.cloud_notm}} account due to IP restrictions, then the user must complete the following steps:

1. Call IBM support at +1 (866) 403-7638.
1. Select the options as required.
1. Request assistance to remove the IP restrictions on your account.
