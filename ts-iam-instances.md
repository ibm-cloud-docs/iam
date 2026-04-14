---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot accessing all instances of a service

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't a user in my account access all instances of a service? 
{: #troubleshoot-instances}
{: troubleshoot}

If a user in your account can't access all instances of a service, you might need to update the type of access they're assigned.
{: shortdesc}

You defined a policy that assigns access to a specific service for a user in your account, but they can't access all instances of the service.
{: tsSymptoms}

You might need to update the access policy. The issue can be caused by the following reasons:
{: tsCauses}

* The user is not included the correct access group.
* The user is not assigned the correct role.
* The access management tag that's defined in the policy isn't correct. The tag in your policy must be the same tag that is attached to the instances of the service.
* The resource has a context-based restriction that excludes the user.

Check the user's level of access.
{: tsResolve}

1. Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select the user from the list on the **Users** page.
2. To view IAM access policies that are assigned to you, select **Access** and view the Access policies table.
3. To determine what access you have through the access groups you are assigned, select **Access** and view the Access groups table. Check the access policies for each of the access groups.

To view what actions are mapped to each role, click the numbers listed next to each role.
{: tip}

To check the name of the access management tag that's attached to the service, complete the following steps:

1. Click the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Resource List**.
2. Locate the service in the table, and see the Tags column.

To help you quickly identify which tags are access management tags, the name is preceded by `IAM` in the label, for example, `IAM | devtools:project1`.
{: tip}

To check the context-based restrictions on a resource, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Rules**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the rule for your service.
1. Click **Details**.
1. Take note of the contexts for the rule. Access is granted by a rule only when at least one of the rule's contexts are satisfied by the user.
