---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-31"

keywords: restrict service id, block users from creating service id, restrict service id creation

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Restricting users from creating service IDs
{: #restrict-service-id-create}

By default, all members of an account can create service IDs. However, access can be restricted so that only members with the correct access can create service IDs by using the Service ID creation setting. For more information about Service IDs, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids).
{: shortdesc}

If service ID creation is [enterprise-managed]{: tag-cyan}, the setting defined at the account-level applies if the enterprise-managed setting is less strict or removed.

## Enabling the restriction to create service IDs in the console
{: #enable-restrict-create-serviceid-ui}
{: ui}

To enable the setting to restrict users from creating service IDs, you must have the following assigned access:

* An IAM policy with the `Administrator`, `Operator`, or `Editor` role on the [IAM Identity Service](/docs/iam?topic=iam-account-services#identity-service-account-management).

If you enable the Restrict service ID creation setting, users in your account require specific access to create service IDs, including the account owner. To restrict who can create service IDs, use the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Settings**.
1. In the Account section, enable **Restrict service ID creation**.
1. Click **Yes** to confirm.

Now that the setting is enabled to restrict users from creating service IDs, you can assign the required access to enable specific users to continue creating service IDs. Remember, the account owner is also required to be assigned this explicit access.
{: important}

## Enabling the restriction to create service IDs by using Terraform
{: #enable-restrict-create-serviceid-terra}
{: terraform}

If you enable the Restrict service ID creation setting, users in your account require specific access to create service IDs, including the account owner.

To enable the setting to restrict users from creating service IDs, you must have the following assigned access:

- An IAM policy with the `Administrator`, `Operator`, or `Editor` role on the [IAM Identity Service](/docs/iam?topic=iam-account-services#identity-service-account-management).

Before you can set limits for login sessions by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

To restrict who can create service IDs, use the following steps:

1. Create an argument in your `main.tf` file. The following example enables the restriction to create service IDs by using the `ibm_iam_account_settings` and `iam_account_settings_instance` resources.
1. Define whether or not creating a service ID restricted. Supported valid values are
   * RESTRICTED - to apply access control
   * NOT_RESTRICTED - to remove access control
   * NOT_SET - to unset a previous set value.

   ```terraform
   resource "ibm_iam_account_settings" "iam_account_settings_instance" {
   restrict_create_service_id  = "RESTRICTED"
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

For more information, see the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_account_settings#restrict_create_service_id).


## Assigning access to create service IDs with restrictions enabled in the console
{: #assign-access-create-service-id-restrict}
{: ui}

If the Service ID creation setting is enabled, only users, including the account owner, assigned the `Service ID creator` role on the IAM Identity Service can create service IDs.

The quickest way to assign a group of users the required access for creating service IDs is to create an access group and assign the group the required role. For more information about assigning access policies, see [Setting up access groups](/docs/iam?topic=iam-groups).
{: tip}
