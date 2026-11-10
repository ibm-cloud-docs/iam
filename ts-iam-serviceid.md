---

copyright:

  years: 2020, 2026
lastupdated: "2026-11-10"

keywords: troubleshoot service ID access, manage service ID permissions, service ID administrator policy, IAM Identity service access, service ID access denied, unable to manage service ID, service ID policy revoked

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I manage a service ID that I created and previously had access to?
{: #troubleshoot-serviceid-access}
{: troubleshoot}
{: support}

Troubleshoot why you cannot manage a service ID that you previously created in an {{site.data.keyword.cloud_notm}} account and learn how to restore the required permissions.
{: shortdesc}

You don't have access to manage a service ID that you created in an account that you're not the owner of. You received an error message about not having the required access, but you used to be able to manage it.
{: tsSymptoms}

If you create a service ID in an account that you don't own, an administrator policy for that specific service ID is automatically generated for you only if you don't already have access to manage service IDs in the account. For example, if you are already assigned the Administrator role on the IAM Identity service, then a new policy is not automatically generated because you already have access. However, if the account administrator later revokes your access as an administrator on the IAM Identity service, then you can no longer manage the service IDs that you created in the account.
{: tsCauses}

Complete the following steps to resolve this issue:
{: tsResolve}

1. Contact the account administrator to request the Editor or Administrator role on the IAM Identity Service, or request an explicit access policy on the specific service ID.
2. After the administrator assigns the policy, go to **Manage** > **Access (IAM)** > **Service IDs** in the {{site.data.keyword.cloud_notm}} console to verify that you can manage the service ID.

For more information, see [Managing service IDs](/docs/iam?topic=iam-serviceids).
