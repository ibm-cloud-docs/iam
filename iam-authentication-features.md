---

copyright:

  years: 2017, 2026
lastupdated: "2026-03-31"

keywords: API keys, service IDs, multifactor authentication, MFA, authentication, identity provider, workload identity, service authentication

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Authentication features
{: #authentication-features}

{{site.data.keyword.cloud}} Identity and Access Management (IAM) provides multiple authentication methods to secure access to your account and resources, including API keys, service IDs, and multifactor authentication (MFA).
{: shortdesc}

## API keys for user authentication
{: #apikey-feature}

You can create multiple API keys for a user to support key rotation scenarios, and the same key can be used for accessing multiple services. {{site.data.keyword.cloud_notm}} API keys enable users who use two-factor authentication or a federated ID to automate authentication to the console from the command line. A user can also have a single classic infrastructure API key that can be used to access classic infrastructure APIs; however, this is not required as you can use {{site.data.keyword.cloud_notm}} API keys to access the same APIs. For more information, see [Understanding API keys](/docs/iam?topic=iam-manapikey).

## Service IDs
{: #svcid-feature}

A service ID identifies a service or application similar to how a user ID identifies a user. These are IDs that can be used by applications to authenticate with an {{site.data.keyword.cloud_notm}} service. Policies can be assigned to each service ID to control the level of access that is allowed by an application that uses the service ID, and an API key can be created to enable the authentication. For more information, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids).

Infrastructure-as-a-Service (IaaS) doesn't support operations that are made by service IDs. If an account includes IaaS and PaaS, administrative functions that are made by a service ID might not work as intended if the operation depends on API calls to IaaS. In an account that includes IaaS, be sure that account administrators complete the administrative functions. For example, functional IDs can be used for administrative functions. In some cases, {{site.data.keyword.IBM_notm}} support might be able to assist with some administrative functions that span both IaaS and PaaS.
{: note}

## MFA
{: #mfa-feature}

You can require MFA for every user in the account or just users with non-federated IDs who do not use SSO. All users with an IBMid use a time-based one-time passcode (TOTP) MFA factor, and any users with a different type of ID must be enabled to use the TOTP, security questions, or external authentication factor separately. For more information, see [Types of multifactor authentication](/docs/iam?topic=iam-types).

## Next steps
{: #authentication-next-steps}

* Learn about [access management features](/docs/iam?topic=iam-access-mgmt-features).
* Explore [trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview) for federated users and compute resources.
* Review [advanced IAM features](/docs/iam?topic=iam-advanced-features) including service authorizations.
