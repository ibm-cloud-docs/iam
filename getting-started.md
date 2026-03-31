---

copyright:

  years: 2017, 2026
lastupdated: "2026-03-31"

keywords: what is IAM, IAM features, IAM API, how IAM works, centralized access management, standards-based, enterprise access control, workload, identity provider, centralized management, fine-grained access, enterprise, layered security architectures, attack surface, SSO, least-privilege access, defense in depth, standards-based identity and access management

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# How {{site.data.keyword.cloud_notm}} Identity and Access Management works
{: #iamoverview}

{{site.data.keyword.cloud}} Identity and Access Management (IAM) provides centralized, standards-based identity and access management with fine-grained access control to implement least-privilege access across your enterprise workloads and reduce your attack surface.
{: shortdesc}

## What is IAM?
{: #what-is-iam}

IAM enables you to securely authenticate users for platform services and control access to resources consistently across {{site.data.keyword.cloud_notm}}. A set of services is enabled to use IAM for access control, and are organized into [resource groups](/docs/account?topic=account-rgs) within your account so you can give users access quickly to more than one resource at a time. Each of these services is labeled as "IAM-enabled" in the catalog. You can use IAM access policies to assign users, service IDs, and trusted profiles access to resources within your account. And, you can group users, service IDs, and trusted profiles into an [access group](/docs/iam?topic=iam-groups) to easily give all members of the group the same level of access.

You can use [trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview) to automate the grouping and granting of access to users, services, and app identities. By specifying conditions based on SAML attributes for users whose identity is federated from your external identity provider (IdP), users can be granted access to resources without having to be invited to the account if they meet those conditions. For service and app identities, you can define fine-grained authorization for all applications that are running in a compute resource without creating service IDs or managing the API key lifecycle for applications.

![IAM access control in an account](images/tp-in-ag-access-diagram.svg){: caption="How IAM access works in an account by using access groups. Service IDs and select {{site.data.keyword.cloud_notm}} can also asssume trusted profiles." caption-side="bottom"}

For classic infrastructure that doesn't support the use of IAM policies for managing access, see the [classic infrastructure permissions](/docs/iam?topic=iam-mngclassicinfra) documentation.
{: note}

## Key IAM features
{: #iam-key-features}

IAM provides a comprehensive set of features to manage access to your {{site.data.keyword.cloud_notm}} resources:

### Access management
{: #iam-access-mgmt}

Control who can access your resources with fine-grained policies, access groups, and time-based conditions. Learn more about [access management features](/docs/iam?topic=iam-access-mgmt-features).

### Trusted profiles
{: #iam-trusted-profiles}

Automate access for federated users and compute resources without managing credentials. Learn more about [trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview).

### Authentication
{: #iam-authentication}

Secure your account with API keys, service IDs, and multifactor authentication. Learn more about [authentication features](/docs/iam?topic=iam-authentication-features).

### Advanced security
{: #iam-advanced-security}

Implement defense in depth with service authorizations and context-based restrictions. Learn more about [advanced IAM features](/docs/iam?topic=iam-advanced-features).

## Getting started with IAM
{: #iam-getting-started}

To start using IAM effectively:

1. **Understand IAM concepts** - Review [IAM access concepts](/docs/iam?topic=iam-access-concepts) and [IAM identities](/docs/iam?topic=iam-identities) to understand the fundamentals.

2. **Plan your access strategy** - Learn about [implementing least privilege access](/docs/iam?topic=iam-least-privilege) and review [IAM policies overview](/docs/iam?topic=iam-policies-overview).

3. **Set up access** - Follow the [IAM quickstart tutorial](/docs/iam?topic=iam-quickstart) to invite users and assign access.

4. **Explore advanced features** - Set up [trusted profiles for federated users](/docs/iam?topic=iam-trustedprofile-fed-tutorial) or [compute resources](/docs/iam?topic=iam-trustedprofile-compute-tutorial).

5. **Enhance security** - Implement [context-based restrictions](/docs/iam?topic=iam-context-restrictions-tutorial) and [multifactor authentication](/docs/iam?topic=iam-types).

## Next steps
{: #iam-next-steps}

* [Learn about access management features](/docs/iam?topic=iam-access-mgmt-features)
* [Explore trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview)
* [Review authentication options](/docs/iam?topic=iam-authentication-features)
* [Discover advanced IAM capabilities](/docs/iam?topic=iam-advanced-features)
