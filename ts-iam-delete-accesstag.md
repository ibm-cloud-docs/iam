---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot permission to delete access management tags

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I delete access management tags?
{: #troubleshoot-delete-accesstag}
{: troubleshoot}

If you can't delete an access management tag within an {{site.data.keyword.Bluemix}} account that you're not the owner of, you might need to check the type of access you're assigned. Or, the tag might be attached to a resource.
{: shortdesc}

* You can't delete access management tags in an account of which you are a member.
* You have the permission, but still unable to delete an access management tag.
{: tsSymptoms}

The action might be blocked by one of the following reasons:
{: tsCauses}

* You might not be assigned the appropriate access to complete the action. You must have the Administrator role on all Account management services.
* The access management tag you're trying to delete is still attached to an active or a reclaimed resource.

Complete the following steps to check your level of access. If you need to request access, contact the account owner.
{: tsResolve}

Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select your name on the **Users** page. 

* To view IAM access policies that are assigned to you, select **Access** and view the Access policies table. 
* To determine what access you have through the access groups you are assigned, select **Access** and view the Access groups table. Check the access policies for each of the access groups.

To view what actions are mapped to each role, click the numbers listed next to each role.
{: tip}

Before you try to delete an access management tag, make sure it's not attached to any of your resources.

* Filter by tag name on your [resource list](/account/tags). If you don't have a viewer permission for all existing resources, contact the account owner to verify.
* Use the **`ibmcloud resource reclamation`** command in the {{site.data.keyword.Bluemix}} CLI to list out resources in reclamation state and delete the resource that had the tag you were trying to delete. For more information, see [Using resource reclamations](/docs/account?topic=account-resource-reclamation).

When you delete an access management tag from the account, any associated IAM policies are also deleted with it.
{: note}
