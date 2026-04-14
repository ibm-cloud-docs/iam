---

copyright:
   years: 2020, 2026
lastupdated: "2026-03-31"

keywords: get started with IAM, getting started with Identity and Access Management tutorial, IAM tutorial, IAM quick start, resource group, access group, access policy, inviting users

subcollection: iam

content-type: tutorial
completion-time: 10m

---

{{site.data.keyword.attribute-definition-list}}

# Assigning access to resources by using access groups
{: #access-getstarted}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Get up and running quickly with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) by setting up access groups for quick access assignments, inviting users to your account, and managing their access.
{: shortdesc}

This tutorial is for IAM-enabled resources. For classic infrastructure that doesn't support creating IAM policies for managing access, you can review the [classic infrastructure permissions](/docs/iam?topic=iam-mngclassicinfra) documentation.
{: note}

## Before you begin
{: #iam-before-you-begin}

If you are new to using IAM, check out the following documentation to learn more about the features, concepts, and components of the access management system:

* [What is IBM Cloud Identity and Access Management?](/docs/iam?topic=iam-iamoverview) provides a quick overview of what IAM is in {{site.data.keyword.cloud_notm}}, the available features, and links to available CLI and API docs.
* [IAM access](/docs/iam?topic=iam-userroles) gives a more in-depth review of how access management works by using access policies.

## Create access groups
{: #create-access-group}
{: step}

To streamline the process of assigning access to users in your account, you can create an access group. Access groups are a way to organize users and service IDs so that you can easily assign access by adding one or more policies for the entire group. Then, you can add or remove users and service IDs as needed instead of assigning individual access to each user.

A unique name is required to differentiate access groups in the account.
{: note}

### Set up your groups
{: #group_setup}

To create an access group, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Access Groups**.
1. Click **Create**.
1. Enter a unique name to identify your access group and an optional description.
1. Click **Create**.

Next, continue to set up your group by adding users or service IDs:

1. Select the name of the group that you want to update.
1. Click **Add users**.
1. Select the users that you want to add from the list, and click **Add to group**.
1. To add service IDs to the group, click **Service IDs**.
1. Select the IDs that you want to add from the list, and click **Add to group**.

### Assign access to your groups
{: #group_access}

After you create your access groups, you can assign access to all members of the group with one or more policies. By assigning a group of users access to a group of resources with a single policy, you reduce the overall number of policies that you need to manage.

1. From the **Access** tab, click **Assign access**.
1. Select a single service or group of services. Then, click **Next**.
1. Scope the access to all resource or specific resources based on attributes. Then, click **Next**.
1. Select the level of access that you want to assign.

   If you're assigning access to IAM-enabled services, some services support the use of advanced operators to grant access to resources that satisfy specific naming conventions. See [Assigning access by using wildcard policies](/docs/iam?topic=iam-wildcard) for more information.
   {: note}

1. Click **Review**.
1. Click **Add** to add your policy configuration to your policy summary.
1. Click **Assign** to assign all added access to your access group.

## Invite users
{: #invite-user}
{: step}

You can invite one or multiple users in a single invite. If you invite multiple users in one invitation, the same access is assigned to each user. However, you can invite users to your account with no access, and assign them access later.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Users**.
1. Click **Invite users**. Specify the email addresses of the users. If you are inviting more than one user with a single invitation, they are all assigned the same access.
1. Add one or more of the access options that you manage. You must assign at least one access option. For any access options that you don't add and configure, the default value of **No access** is assigned. Depending on the options that you are authorized to manage, you can assign the following types of access:

   * Access groups: Click **Add** for each access group that you want the users to belong to.
   * Access policy: Assign individual IAM access policies or classic infrastructure permissions.
     * Select **Classic infrastructure**, and then select from the three permission sets.
     * Select a group of services like **All Identity and Access enabled services**, **All Account Management services**, and **All IAM Access Management services**, or select a specific service. Next, you can scope the access to the entire account or just one resource group. Then, select all roles that apply. To view what actions are mapped to each role, click the numbers listed next to each role.

         Some services support the use of advanced operators to grant access to resources that satisfy specific naming conventions. See [Assigning access by using wildcard policies](/docs/iam?topic=iam-wildcard) for more information.

1. Then, select all roles that apply.
1. Select **Add** to save the access assignment to the invitation.
1. After you add all the necessary access assignments, click **Invite**.

For more information, see [Inviting users to an account](/docs/iam?topic=iam-iamuserinv).

## Manage access for existing users
{: #user_access_manage}
{: step}

After you invite users, you might want to assign more access or edit the existing access to ensure that all members of your account have the correct level of access.

### Assigning new access
{: #new_access}

To assign a new access policy, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Users**.
1. From the row for the user that you want to assign access, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Assign access**.
1. Select a service or group of services. Then, click **Next**.
1. Scope the access to all resources or specific resources based on selected attributes. Then, click **Next**.
1. Select any combination of roles or permissions to define the scope of access, and click **Review**. For more information, see [IAM roles](/docs/iam?topic=iam-userroles#iamusermanrol).
1. Click **Add** to add your policy configuration to your policy summary.
1. Click **Assign** to assign all added access to the selected user.

Assign the viewer role or higher to the resource group that contains the resource to ensure that the user can access the resource from their list of resources.
{: tip}

### Editing existing access
{: #editing_access}

You can update existing access by editing the assigned roles for a user.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Users**.
1. Select the name of the user that you want to edit access for.
1. Click **Access**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit** on the row for the policy that you want to edit.
1. Edit the policy by updating the assigned roles.
1. Click **Save**.

## Next steps
{: #iam-user-next}

Continue securing your cloud resources by creating context-based restrictions, which work with traditional IAM policies, to provide another layer of protection.
