---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: dashboard, custom dashboard

subcollection: iam
---

{{site.data.keyword.attribute-definition-list}}

# Best practices for cross-account access
{: #bp-cross-account}

Your organization might need to collaborate across different accounts within the enterprise, or with other companies outside of your organization. You can securely provide users and service IDs from one account access to resources in another account by using the REST APIs.

Cross-account policies can be created only by using the API. The console and CLI accept only subjects from the same account as the resource. However, you can view the cross-account policies in the console and CLI after you create them.
{: preview}

## Creating cross-account policies
{: #create-cross-acc-policy}

Using IAM policies, you can grant users and service IDs in one account access to IBM Cloud resources in another account.

### Use case for cross-account access for federated users
{: #cross-acc-fed-users}

As an Administrator of a resource, you might need to grant access to resources in your account to federated users in another account within your enterprise. As a federated user, you need access to resources in an account that you're not a member of so that you can collaborate on a project.

For this use case, use trusted profiles. A trusted profile can be granted access to any resources in the same account using access policies. Once the access is granted to the trusted profile, federated users can be granted the ability to “apply” the trusted profile by establishing trust. Trust rules do not require that the federated users be members of any specific account. The federated user can log in and apply the trusted profile to gain the access they need.


## Viewing cross-account policies in the console
{: #view-cross-acc-ui}
{: ui}

## Viewing cross-account policies by using the CLI
{: #view-cross-acc-cli}
{: cli}

## Viewing cross-account policies by using the API
{: #view-cross-acc-api}
{: api}
