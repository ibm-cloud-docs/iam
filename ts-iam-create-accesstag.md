---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot permission to create access management tags

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I create access management tags?
{: #troubleshoot-create-accesstag}
{: troubleshoot}

If you can't create an access management tag within an {{site.data.keyword.Bluemix}} account that you're not the owner of, you might need to check the type of access you're assigned.
{: shortdesc}

You can't create access management tags in an account of which you are a member. 
{: tsSymptoms}

This problem can commonly occur by one of the following reasons:
{: tsCauses}

* You might not be assigned the appropriate access to complete the action. You must have the Administrator role on all Account management services.
* You reached the limit of 250 access management tags per account.
* Some services don't have full support for access management tags on their UI, so when you're creating an instance of those services, you can only attach user tags. To learn how you can work with access management tags, see the tutorial about [controlling access to resources by using tags](/docs/account?topic=account-access-tags-tutorial).

Complete the following steps to check your level of access. If you need to request access, contact the account owner.
{: tsResolve}

Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select your name on the **Users** page.

* To view IAM access policies that are assigned to you, select **Access** and view the Access policies table.
* To determine what access you have through the access groups you are assigned, select **Access** and view the Access groups table. Check the access policies for each of the access groups.

To view what actions are mapped to each role, click the numbers listed next to each role.
{: tip}
