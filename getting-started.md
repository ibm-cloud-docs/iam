---

copyright:

  years: 2017, 2026
lastupdated: "2026-03-31"

keywords: what is IAM, IAM features, IAM API, how IAM works, centralized access management, standards-based, enterprise access control, workload, identity provider, centralized management, fine-grained access, enterprise, layered security architectures, attack surface, SSO, least-privilege access, defense in depth, standards-based identity and access management

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# What is {{site.data.keyword.cloud_notm}} Identity and Access Management?
{: #iamoverview}

{{site.data.keyword.cloud}} Identity and Access Management (IAM) provides centralized, standards-based identity and access management with fine-grained access control to implement least-privilege access across your enterprise workloads and reduce your attack surface.
{: shortdesc}

Securely authenticate users for platform services and control access to resources consistently across {{site.data.keyword.cloud_notm}}. A set of services is enabled to use IAM for access control, and are organized into [resource groups](/docs/account?topic=account-rgs) within your account so you can give users access quickly to more than one resource at a time. Each of these services is labeled as "IAM-enabled" in the catalog. You can use IAM access policies to assign users, service IDs, and trusted profiles access to resources within your account. And, you can group users, service IDs, and trusted profiles into an access group to easily give all members of the group the same level of access.

You can use trusted profiles to automate the grouping and granting of access to users, services, and app identities. By specifying conditions based on SAML attributes for users whose identity is federated from your external identity provider (IdP), users can be granted access to resources without having to be invited to the account if they meet those conditions. For service and app identities, you can define fine-grained authorization for all applications that are running in a compute resource without creating service IDs or managing the API key lifecycle for applications.

![IAM access control in an account](images/tp-in-ag-access-diagram.svg){: caption="How IAM access works in an account by using access groups. Service IDs and select {{site.data.keyword.cloud_notm}} can also asssume trusted profiles." caption-side="bottom"}

For classic infrastructure that doesn't support the use of IAM policies for managing access, see the [classic infrastructure permissions](/docs/iam?topic=iam-mngclassicinfra) documentation.
{: note}

## Key IAM features
{: #iam-key-features}

IAM provides a comprehensive set of features to manage access to your {{site.data.keyword.cloud_notm}} resources:

### Access management
{: #iam-access-mgmt}

Control who can access your resources with fine-grained policies, access groups, and time-based conditions. For more details, see [access management features](/docs/iam?topic=iam-access-mgmt-features).

### Trusted profiles
{: #iam-trusted-profiles}

Automate access for federated users and compute resources without managing credentials. For more details, see [trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview).

### Authentication
{: #iam-authentication}

Secure your account with API keys, service IDs, and multifactor authentication. For more details, see [authentication features](/docs/iam?topic=iam-authentication-features).

### Advanced security
{: #iam-advanced-security}

Implement defense in depth with service authorizations and context-based restrictions. For more details, see [advanced IAM features](/docs/iam?topic=iam-advanced-features).

## Getting started with IAM
{: #iam-getting-started}

Complete the following steps to start using IAM effectively:

1. Review [IAM access concepts](/docs/iam?topic=iam-access-management-overview) and [IAM identities](/docs/iam?topic=iam-identity-overview) to understand the fundamentals.
2. Plan your access strategy by learning about [least privilege access](/docs/iam?topic=iam-least-privilege) and reviewing [IAM policies overview](/docs/iam?topic=iam-iamusermanpol).
3. Follow the [Assigning access quickstart tutorial](/docs/iam?topic=iam-access-getstarted) to invite users and assign access to your account.
4. Set up [trusted profiles for federated users](/docs/iam?topic=iam-trustedprofile-fedusers-tutorial) or [compute resources](/docs/iam?topic=iam-trustedprofile-compute-tutorial).
5. Implement [context-based restrictions](/docs/iam?topic=iam-context-restrictions-tutorial) and [multifactor authentication](/docs/iam?topic=iam-types) for enhanced security.
