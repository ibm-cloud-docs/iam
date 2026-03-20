---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: dynamic rules,access groups,specific identity attributes,identity provider,federated ID,

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Creating dynamic rules for access groups
{: #rules}

You can create dynamic rules to automatically add federated users to access groups based on specific identity attributes. When your users log in with a federated ID, the data from the identity provider (IdP) dynamically maps your users to an access group based on the rules that you set.
{: shortdesc}

Users already have specific identity information within your company's domain, and when they log in with a federated ID, this data can be passed through by using SAML assertions. The SAML assertions or attribute statements that are configured within the IdP provide the data that is used to create each rule. For example, you might have a true or false attribute statement that defines users as a manager. This information can be used to add all users who are managers to a specific access group for managers that you created in your {{site.data.keyword.Bluemix}} account. For more information, see the tutorial about how to [Control access to cloud resources](https://developer.ibm.com/articles/identity-and-access-management-what-developers-need-to-know/){: external} and an [Example rule](/docs/account?topic=account-rules#example).

Only users who are already invited to the account can be mapped to access groups by using dynamic rules.
{: note}

## Setting up rules by using the console
{: #setup_rules}
{: ui}

Dynamic rules are created by setting conditions that must be matched by the data that is configured within the IdP and passed in with a user's federated ID during login. You can add more than one condition for a rule. All conditions set in the rule must be met for a user to be added to an access group.

To create a rule, follow these steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Access Groups**.
2. Select the name of the access group that you want to create a rule for. This action opens the group **Details** page.
3. Select **Dynamic rules**.
4. Click **Add rule**.
5. Enter the information from your IdP that is dynamically provided for you on the Add rule page. The following list provides details for each required field.

You can think of an access group rule as a key:value pair. The key is what you add in the `Add users when` field, and the value is what you enter in the `Values` field.
{: tip}

For more information about the fields that are used to create dynamic rules, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).

## Setting up rules by using Terraform
{: #setup_rules_terraform}
{: terraform}

Before you can set up rules by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Dynamic rules are created by setting conditions that must be matched by the data that is configured within the IdP and passed in with a user's federated ID during login. You can add more than one condition for a rule. All conditions set in the rule must be met for a user to be added to an access group.

To create a rule by using Terraform, follow these steps:

1. Create an argument in your `main.tf` file. The following example creates a new dynamic rule for an access group by using the `ibm_iam_access_group_dynamic_rule` resource, where `name` is a unique name to identify the dynamic rule.

   ```terraform
    resource "ibm_iam_access_group_dynamic_rule" "rule1" {
      name              = "newrule"
      access_group_id   = "AccessGroupId-dsnd4bvsaf"
      expiration        = 4
      identity_provider = "test-idp.com"
      conditions {
        claim    = "blueGroups"
        operator = "CONTAINS"
        value    = "\"test-bluegroup-saml\""
      }
    }
   ```
   {: codeblock}

   For more information, see the argument reference details in the [Terraform documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_access_group_dynamic_rule) page.

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

For more information about the fields that are used to create dynamic rules, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).

## Viewing dynamic members of access groups
{: #view-dynamic-users}
{: ui}

You can view the users that are added to an access group by using dynamic rules. To view dynamic members of access groups, go to **Manage** > **Access (IAM)** > **Access groups** in the {{site.data.keyword.cloud_notm}} console. Select an access group and click **Users**. Dynamically added users are indicated by the type `Dynamic`.

The following users will not appear in the table:

- Dynamically added users who are not logged in yet.
- Dynamically added users whose session expired.

Dynamic users that are logged out but whose sessions are still valid continue to appear in the table until their sessions expire.

You can't remove a dynamic user manually. To remove a dynamic user, adjust your dynamic rules.
{: note}

### Viewing a user's dynamic membership
{: #view-dynamic-ag}

You can also view a list of access groups that a user is added to based on dynamic rules by completing the following steps:

1. Go to **Manage** > **Access (IAM)** > **Users** in the {{site.data.keyword.cloud_notm}} console.
1. Click on a user.
1. Click **Access**.
1. The access groups that a user is a dynamic member of is indicated by the type `Dynamic`.

## Example rule
{: #example}

The following example includes values for each of the fields for a dynamic rule. In this rule, users who are identified as managers within the federated IdP are mapped to an {{site.data.keyword.cloud_notm}} access group that has specific access set for only managers.

| Field                           | Value                           |
|---------------------------------|---------------------------------|
| Name                            | Manager group rule              |
| Identity provider               | `https://idp.example.org/SAML2` |
| Expiration (in hours)           | 12                              |
| Add users when (attribute name) | isManager                       |
| Comparator                      | Equals                          |
| Value                           | true                            |
{: caption="Example dynamic rule for access groups" caption-side="top"}
