---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot manage service id, can't manage service id

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I manage a service ID that I created and previously had access to?
{: #troubleshoot-serviceid-access}
{: troubleshoot}

In the case that you aren't able to manage a service ID that you created in another user's account, you might need to check your assigned access.
{: shortdesc}

You don't have access to manage a service ID that you created in an account that you're not the owner of. You received an error message about not having the required access, but you used to be able to manage it.
{: tsSymptoms}

If you create a service ID in an account that you don't own, an administrator policy for that specific service ID is automatically generated for you only if you don't already have access to manage service IDs in the account. For example, if you are already assigned the Administrator role on the IAM Identity service, then a new policy is not automatically generated because you already have access. However, if the account administrator later revokes your access as an administrator on the IAM Identity service, then you can no longer manage the service IDs that you created in the account.
{: tsCauses}

Request the correct level of access from the account administrator to manage all service IDs in the account or just the specific ones that you created. 
{: tsResolve}
