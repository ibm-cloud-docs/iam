---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot account, dashboard role, permission, view dashboard, dashboard

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why did the creation of an alternative account owner trusted profile fail?
{: #ts_alt-owner}
{: troubleshoot}

You're unable to create an alternative account owner trusted profile because only one can be set per account.
{: shortdesc}

A trusted profile is created without the classic infrastructure permissions that an alternative account owner is normally assigned. You receive an error after you create the trusted profile.
{: tsSymptoms}

```text
An error occured while trying to apply the admin flag for this account. An error occurred. Try again later. Only 1 TrustedProfile per account may be set as the alternate master user.
```

You might already have an alternative account owner trusted profile in the account. You can set only one trusted profile as the alternative account owner.
{: tsCauses}

Delete the trusted profile that has an error. Check the account for an existing trusted profile with alternative account owner access, an `alt account owner` tag. If no such profile exists, try creating the trusted profile again.
{: tsResolve}

For more information, see [Setting an alternative account owner](/docs/account?topic=account-transfer).
