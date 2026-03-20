---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: maximum limits, limits, service ID, increase service ID limit, API key, IdP, trusted profile, identity, entity

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Increasing limits for IAM Identity entities 
{: #increase-entity-limit}

WIP

{{site.data.keyword.cloud_notm}} accounts have default limits for different entities like service IDs, trusted profiles, IdPs, or API keys. However, there can be specific use cases that require an extended limit and you need to request an increase for your chosen entity. For more information on the {{site.data.keyword.cloud_notm}} IAM limits, see [Known issues and limitations](/docs/account?topic=account-known-issues).
{: shortdesc}

When your account starts to reach the maximum limit of one of the entities, you receive a warning in the activity tracking events for creating an entity. These events show you the current limits. See the following example:

```text
Nov 26 16:46:01 iamid-6-11-12270-af4d601-cd77fd6bd-86gp7 at.log INFO IAM Identity Service: create account-serviceid 12345678-90ab-cdef-0123-456789abcdef -failure Warning: You have reached 100% of the maximum number of allowed Service IDs in account 11112222333344445555666677778888. Your current count is 3000, and the limit is 3000.
```

## Before you begin
{: #prereqs-increase}

A limit increase can be requested for the following types of entities:

* API keys per identity
* Service IDs
* IdPs
* Trusted Profiles

You can request a limit increase for the chosen entities only if the following criteria is met:

* You must be the account owner or an administrator on all account management services.
* You have taken efforts to clean up and reduce the number of entities in the account.
* You must have a specific, reasonable use case for requesting an increase. 

## Requesting a limit increase for different entities
{: #request-limit-increase-entity}

If you meet all of the previously listed criteria, you can request a limit increase for the chosen entities by submitting a support case in the [console](/unifiedsupport/cases/add){: external}. In the case, provide all of the following information. Each piece of information is required for processing and approval of your request. 

* Case title of `Request to increase account <entity> limit`
* The use case for the limit increase
* Information on all efforts taken to reduce the number of `<entities>` on the account
* Account ID
* Note how many extra `<entities>` in the account are required

When the request is approved, the IAM team changes the limits for your account.
  
You are notified of the update to your entity limits through the case.
{: note}




