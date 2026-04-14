---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot permission to attach and detach access management tags

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I attach or detach access management tags on a resource?
{: #troubleshoot-attach-detach-accesstag}
{: troubleshoot}

If you can't attach or detach access management tags on a resource, you might need to check the following items:

* List of the existing tags
* The type of access you're assigned
* Type of the resource
{: shortdesc}

You can't attach or detach access management tags on a resource, which you have access to.
{: tsSymptoms}
   
This problem can be commonly caused by the following reasons:
{: tsCauses}

* You're trying to attach an access management tag that doesn't exist yet in the account, which you are a member of. You need to [create the access management tag](/account/tags) first.
* You might not be assigned the appropriate access to complete the actions. You must have the Administrator role on the resource.
* The resource is not an IAM-enabled resource. Only a set of {{site.data.keyword.Bluemix}} services is enabled to use {{site.data.keyword.Bluemix}} IAM for access control. These services need to be labeled as "IAM-enabled" in the catalog.
* Some services don't have full support for access management tags on their UI, so when you're creating an instance of those services, you can only attach user tags. To learn how you can work with access management tags, see the tutorial about [controlling access to resources by using tags](/docs/account?topic=account-access-tags-tutorial).

Complete the following steps to check your level of access. If you need to request access, contact the account owner.
{: tsResolve}

Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select your name on the **Users** page.

* To view IAM access policies that are assigned to you, select **Access** and view the Access policies table. 
* To determine what access you have through the access groups you are assigned, select **Access** and view the Access groups table. Check the access policies for each of the access groups.

To view what actions are mapped to each role, click the numbers listed next to each role.
{: tip}
