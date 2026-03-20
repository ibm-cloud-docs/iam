---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: custom access, custom role, create a role, combine actions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Creating custom roles
{: #custom-roles}

Each service maps specific actions that you can perform within the context of the service to platform or service roles. From the Roles page in {{site.data.keyword.Bluemix}} Identity and Access Management (IAM), you can view all of the available roles in the account and all roles for a specific service, including the actions that are mapped to each. You can pick and choose actions from all of the roles for a specific service to combine into a custom role of your choice.
{: shortdesc}

Many services map different sets of actions to different platform or service roles. However, you might want to combine some of the actions that are currently spread across multiple roles for a service to make assigning meet your custom use case. For example, with a custom role, you can pick and choose actions that are mapped to different roles so that next time you assign access to the service, you don't must select three different roles.

As a unique usage scenario, you can create your own custom roles for controlling access management tags. It is possible to separate the permissions for attaching and detaching access management tags on the resources. For example, you can create a custom role where a user can attach access management tags to resources, but it does not allow them to remove those tags from them and vice versa.

Creating two roles with different names but the exact set of actions fail. IAM treats roles with identical permissions as duplicates, even if their names are unique.
{: note}

## Required access
{: #required-access-role-management}

Anyone can view the available roles in the account on the **Roles** page, but to create, edit, or delete a custom role, you must be assigned specific access for the Role management account management service.

| Role | Actions |
|------|---------|
| Editor |  Can edit and update the role display name, description, and the actions mapped to it.   |
| Administrator | Create, edit, update, and delete custom roles and assign other users in the account access to the Role management service |
{: caption="Actions for Role management service" caption-side="top"}

## Creating custom roles in the console
{: #custom-access-roles}
{: ui}

You can create new roles that are scoped to single services. This means that you can't combine actions for two different services in a custom role, but you can combine as many actions that you want into a new role for a single service. After you create a custom role with a name of your choosing, anyone in the account who can assign access to a particular service can use that role when assigning access.

Custom roles can be created only for individual IAM-enabled services. A custom role can't be created for the options of all account management services or all IAM-enabled services.
{: note}

1. In the {{site.data.keyword.cloud}} console, go to **Manage** > **Access (IAM)**, and select **Roles**.
1. Click **Create**.
1. Enter a name for your role. This name must be unique within the account. Users see this role name in the console when they assign access to the service.
1. Enter an ID for the role. This ID is used in the CRN, which is used when assigning access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only.
1. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the console when a user assigns access to the service.
1. Select a service that you want to create the role for.
1. Review the available actions, and select **Add** for all actions that you want in your new role.

   Add at least one service-defined action to successfully create the new role. If you aren't sure which actions are defined by the service, look in the Type column.
   {: important}

1. Click **Create** when you're done adding actions.

If a service removes an action that you use in a custom role, the custom role is not updated, and might not be valid anymore if the role contained only the removed actions.
{: note}

If you plan to delete a custom role because it is no longer needed, you must be assigned the Administrator role on the Role management service. Deleting a custom role automatically updates access for any users, access groups, or service IDs assigned access by using that role to remove it from any existing policies.

## Creating custom roles by using Terraform
{: #custom-access-roles-terraform}
{: terraform}

Before you can create custom roles by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create custom roles:

1. Create an argument in your `main.tf` file. The following example creates a custom role by using the `ibm_iam_custom_role` resource, where `name` is a unique name to identify the custom role. Add at least one service-defined `action` to successfully create the new role.

   ```terraform
   resource "ibm_iam_custom_role" "customrole" {
    name         = "Role1"
    display_name = "Role1"
    description  = "This is a custom role"
    service = "kms"
    actions      = ["kms.secrets.rotate"]
   }
   ```
   {: codeblock}

   You can specify the name of the service for which you want to create the custom role on the `service` option. For more information, see the argument reference details on the [Terraform Identity and Access Management (IAM)](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_custom_role){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
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
