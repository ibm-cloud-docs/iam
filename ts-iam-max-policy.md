---

copyright:
  years: 2020, 2026
lastupdated: "2026-03-31"

keywords: troubleshoot maximum policies, what do I do when I reach too many policies, exceed policies count

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is a policy limit blocking me from assigning access?
{: #troubleshoot-policy-limit}
{: troubleshoot}

You might encounter an error when you're assigning access if you already have the maximum number of policies in your {{site.data.keyword.Bluemix}} account.
{: shortdesc}

You tried to assign access, but received an error message that you reached the limit of access policies in the account.

A new policy can't be created to assign access, and you receive an error message that states:
{: tsSymptoms}

```text
422: Exceeded maximum policies quota error
```

The account is at the [limit of the total number of policies allowed](/docs/iam?topic=iam-known-issues).
{: tsCauses}

Reduce the number of policies on the account by following the [Best practices for organizing resources and assigning access](/docs/account?topic=account-account_setup). For more information about policy limits for the account, see [IBM Cloud IAM limits](/docs/iam?topic=iam-known-issues).
{: tsResolve}
