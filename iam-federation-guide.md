---

copyright:

  years: 2023, 2026
lastupdated: "2026-04-06"

keywords: SAML federation, federation option, federated IBMid, SAML fed, federated, identity provider integration, SSO, single sign-on

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Integrating your identity provider with {{site.data.keyword.cloud_notm}}
{: #federation-option-for-you}

Connect your corporate identity provider to {{site.data.keyword.cloud_notm}} using SAML federation. Enable single sign-on (SSO) for users with IBMid or App ID integration.
{: shortdesc}

{{site.data.keyword.cloud_notm}} supports integration with customer's user directories by using IBMid SAML federation, the {{site.data.keyword.cloud_notm}} SAML service provider, or your own instance of {{site.data.keyword.appid_full_notm}}.

By default, when you create an account in {{site.data.keyword.cloud_notm}} you use an IBMid for user identity. IBMid is the ID as a Service (IDaaS) from {{site.data.keyword.IBM_notm}} used to access {{site.data.keyword.IBM_notm}} web-based services, including {{site.data.keyword.cloud_notm}} resources. The IBMid is based on your company's email address and a password that is managed by IBMid. IBMid allows you to federate to your own corporate user directory or a third-party Identity Provider (IdP) service that you might already use, such as Okta.

<production>Federating to your own directory simplifies the process of adding users to your account, without requiring an IBMid with a separate password. However, there are cases where it might not be feasible for you to use IBMid to federate your corporate user directory. The alternative is to create an {{site.data.keyword.appid_full_notm}} instance in your account and connect it to your chosen IdP.

This topic explains the differences between the following two methods:
   * Federating with IBMid.
   * Federating with your own instance of {{site.data.keyword.appid_full_notm}}.</production><idp>

Federating to your own directory simplifies the process of adding users to your account, without requiring an IBMid with a separate password. However, there are cases where it might not be feasible for you to use IBMid to federate your corporate user directory. Two alternatives exist: create an {{site.data.keyword.appid_full_notm}} instance in your account and connect it to your chosen IdP or use the {{site.data.keyword.cloud_notm}} SAML service provider (SP).

This topic explains the differences between the following three methods:
   * Federating with IBMid.
   * Federating with your own instance of {{site.data.keyword.appid_full_notm}}.
   * Federating with the {{site.data.keyword.cloud_notm}} SAML SP.</idp>



To decide which option is applicable to your use case, review the following sections.

## Which SAML federation options exist in {{site.data.keyword.cloud_notm}}?
{: #federation-options}

{{site.data.keyword.cloud_notm}} supports the following user types:

Non-federated IBMid users
:   Users with a valid email address can create an IBMid and let IBMid manage the password. Your company email domain is not federated with IBMid, and you choose to keep it as is. Any user that uses your email domain can create their own IBMid, and the password they create is managed by IBMid. They can create an {{site.data.keyword.cloud_notm}} account and invite other users with an IBMid to their account. They can also access other {{site.data.keyword.IBM_notm}} web offerings by using that same IBMid.

<production>Federated IBMid users
:   Enterprise customers often connect their internal user directory, or IdP, with IBMid so that their employees don't need to manage an additional password. Instead, they can reuse their normal login to their IdP to log in to {{site.data.keyword.IBM_notm}} web offerings, including {{site.data.keyword.cloud_notm}}. Connecting an external IdP with IBMid is called federation, and the technical underlying protocol is called SAML. Those users are often referenced as federated IBMid users. As IBMid is federating with multiple enterprise customers at the same time, one prerequisite of a successful federation is a unique email address for each IBMid user.</production>

{{site.data.keyword.appid_full_notm}} users
:   Instances of the {{site.data.keyword.appid_full_notm}} can also connect to an IdP. An {{site.data.keyword.appid_short}} instance can connect to only one external IdP using SAML, and therefore a unique email address isn't required.<idp>

Federated {{site.data.keyword.cloud_notm}} SAML users
:   {{site.data.keyword.cloud_notm}}'s SAML SP enables SAML-based federation with your own identity provider. Unlike IBMid federation, which connects users through {{site.data.keyword.IBM_notm}}’s identity system, or {{site.data.keyword.appid_full_notm}}, which requires a searate service instance, the {{site.data.keyword.cloud_notm}} SAML SP integrates directly with your enterprise IdP in the IAM console for secure access to {{site.data.keyword.cloud_notm}} services.

![A diagram that shows the relationship between the {{site.data.keyword.cloud_notm}} SAML service provider, your enterprise IdP, and your users logging into {{site.data.keyword.cloud_notm}}.](images/service-provider-idp.svg){: caption="A diagram that shows the relationship between the {{site.data.keyword.cloud_notm}} SAML service provider, your enterprise IdP, and your users logging into {{site.data.keyword.cloud_notm}}." caption-side="bottom"}</idp>

## {{site.data.keyword.cloud_notm}} account owners
{: #owner-v-members}

To create an {{site.data.keyword.cloud_notm}} account, you need an IBMid user that will be the {{site.data.keyword.cloud_notm}} account owner. You can create this IBMid user during the [{{site.data.keyword.cloud_notm}} account registration process](https://{DomainName}/registration), or you use an existing IBMid user. We recommend creating the account by using a [functional ID](/docs/iam?topic=iam-identity-overview#functionalid-bestpract) or service account with a valid email address, this can help simplify account ownership continuity in your organization.

<production>For any additional members of your {{site.data.keyword.cloud_notm}} account, you have the option to use normal or federated IBMid users as {{site.data.keyword.cloud_notm}} account members. Alternatively, you can connect your IdP to your {{site.data.keyword.cloud_notm}} account by using an {{site.data.keyword.appid_full_notm}} service instance. All users that log in through that {{site.data.keyword.appid_full_notm}} service instance are added to your account automatically, so you don't need to invite those users.</production><idp>For any additional members of your {{site.data.keyword.cloud_notm}} account, you have the option to use normal or federated IBMid users as {{site.data.keyword.cloud_notm}} account members. Alternatively, you can connect your IdP to your {{site.data.keyword.cloud_notm}} account by using the {{site.data.keyword.cloud_notm}} SAML SP or an {{site.data.keyword.appid_full_notm}} service instance. All users that log in through the {{site.data.keyword.cloud_notm}} SAML SP or that {{site.data.keyword.appid_full_notm}} service instance are added to your account automatically, so you don't need to invite those users.</idp>

## How do you onboard {{site.data.keyword.cloud_notm}} account members?
{: #federation-onboarding}

{{site.data.keyword.cloud_notm}} accounts have access to all IBMid users, federated and non-federated. IBMid users must be invited to your {{site.data.keyword.cloud_notm}} account. As a consequence, the same IBMid user can be member of multiple {{site.data.keyword.cloud_notm}} accounts at the same time. In the {{site.data.keyword.cloud_notm}} console, the IBMid user can select the account in which this user is working.

<production>During configuration of your {{site.data.keyword.appid_full_notm}} service instance, you connect the service instance with your {{site.data.keyword.cloud_notm}} account. Therefore, users that log in by using this service instance can be member of this only one account. Those users will be automatically added to your {{site.data.keyword.cloud_notm}} account when they authenticate the first time.</production><idp>During configuration of the {{site.data.keyword.cloud_notm}} SAML SP or your {{site.data.keyword.appid_full_notm}} service instance, you connect the IdP to your {{site.data.keyword.cloud_notm}} account. Therefore, users that log in by using the {{site.data.keyword.cloud_notm}} SAML SP or the {{site.data.keyword.appid_full_notm}} service instance can be member of this only one account. Those users are automatically added to your {{site.data.keyword.cloud_notm}} account when they authenticate the first time.</idp>

## Comparing federation options
{: #choose-federation}

<production>The following table compares characteristics of each federation option. In both cases, the assumption is that the customer connects either an IBMid or an {{site.data.keyword.appid_full_notm}} instance with their IdP with SAML.

| Feature |IBMid|{{site.data.keyword.appid_short}}|
|---|---|---|
|Email address|Users must have a globally unique email address. For example, firstname.lastname@example.com. If your company's email domain is already federated, you can start configuring access to your account. If it's not already federated, a manual process with the IBMid federation team is required to establish federation. During the federation setup process, the customer collaborates with the IBMid federation team to define which email pattern matches with the IdP users. The decision to federate to your company's own user directory needs to involve the person in your company that can make company-wide decisions when it comes to connecting to external parties for identity services. You need to ensure that this person is included in the process. Federating with IBMid can have an impact on non-{{site.data.keyword.cloud_notm}} web services that your company already uses with {{site.data.keyword.IBM_notm}}.|This option requires the creation of an {{site.data.keyword.appid_short}} instance. It is a self-service option with a low usage fee. Choosing this option requires a custom URL to log in to {{site.data.keyword.cloud_notm}}. In addition, an {{site.data.keyword.appid_short}} instance and configuration of the federation to your IdP is required for every {{site.data.keyword.cloud_notm}} account.|
|Costs|Customers do not need to pay to use IBMid with or without federation.| {{site.data.keyword.appid_full_notm}} instances have a low fee, with a free tier up to 1,000 users and 1,000 events (for example, logins). See the {{site.data.keyword.appid_short}} page for more details.|
| Federation setup| Customers need to open a support case with IBMid Enterprise Federation to start the onboarding process. This is a manual process.| Customer creates an {{site.data.keyword.appid_full_notm}} instance and configures it according to the documented steps. This process is self-service.|
| Federation maintenance (for example, certificate update)| Requires a manual interaction with the IBMid federation team.| The customer can update their {{site.data.keyword.appid_full_notm}} instance on their own (for example, this step is self-service).|
| Federation scope| IBMid federation applies to every service that uses IBMid. This means that if a customer onboards to IBMid federation, this applies to his employees when logging on to {{site.data.keyword.cloud_notm}}, but also when using other {{site.data.keyword.IBM_notm}} SaaS offerings that are using IBMid.| The federation has impact only on the {{site.data.keyword.cloud_notm}} account in which the {{site.data.keyword.appid_full_notm}} instance is configured to allow logins. It also does not impact any other {{site.data.keyword.cloud_notm}} accounts or IBM SaaS offerings.|
| Account member onboarding| Users need to be invited by their email address.| Each user that can successfully log in to the configured {{site.data.keyword.appid_full_notm}} instance will automatically be added to the {{site.data.keyword.cloud_notm}} account.|
| Cross-account membership| IBMids can be members of multiple accounts.| Users can be members of one account only. Even if multiple {{site.data.keyword.appid_full_notm}} instances federate to the same IdP, the users are treated as separate users in each account.|
| Use of SAML assertions in access group or trusted profile dynamic rules| Any SAML assertion sent by the IdP can be used in access group or trusted profile dynamic rules.| Any SAML assertion sent by the IdP can be used in access group or trusted profile dynamic rules.|
| Reliability| IBMid is a global service with a dedicated operations team. In case of an outage in a data center, IBMid can failover to a different data center.| Depends on the user's IdP high availability and failover setup.| Any {{site.data.keyword.appid_full_notm}} instance exists in one region. Failures in that region can prevent account members from being able to log in. Users that are already logged in are usually not affected by such a failure.|
| Login behavior| Users log in by using the central login page.| You need to use a special URL to log in to your {{site.data.keyword.cloud_notm}} account. Your account administrator gets this URL from the IAM [Identity providers](/iam/identity-providers) page in the {{site.data.keyword.cloud_notm}} console.|</production>

<idp>The following table compares characteristics of each federation option. In all cases, the assumption is that the customer connects their IdP to the {{site.data.keyword.cloud_notm}} SAML SP, an IBMid, or an {{site.data.keyword.appid_full_notm}} instance with SAML.

| Feature | IBMid | {{site.data.keyword.cloud_notm}} SAML SP | {{site.data.keyword.appid_short}}|
|---|---|---|---|
|Email address|Users must have a globally unique email address. For example, firstname.lastname@example.com. If your company's email domain is already federated, you can start configuring access to your account. If it's not already federated, a manual process with the IBMid federation team is required to establish federation. During the federation setup process, the customer collaborates with the IBMid federation team to define which email pattern matches with the IdP users. The decision to federate to your company's own user directory needs to involve the person in your company that can make company-wide decisions when it comes to connecting to external parties for identity services. You need to ensure that this person is included in the process. Federating with IBMid can have an impact on non-{{site.data.keyword.cloud_notm}} web services that your company already uses with {{site.data.keyword.IBM_notm}}.| The user's email address is a required attribute for authentication. This ensures that {{site.data.keyword.cloud_notm}} can associate the authenticated user with their account and permissions.|This option requires the creation of an {{site.data.keyword.appid_short}} instance. It is a self-service option with a low usage fee. Choosing this option requires a custom URL to log in to {{site.data.keyword.cloud_notm}}. In addition, an {{site.data.keyword.appid_short}} instance and configuration of the federation to your IdP is required for every {{site.data.keyword.cloud_notm}} account.|
|Costs|Customers do not need to pay to use IBMid with or without federation.| Using the {{site.data.keyword.cloud_notm}} SAML SP to federate users from your IdP has no cost. | {{site.data.keyword.appid_full_notm}} instances have a low fee, with a free tier up to 1,000 users and 1,000 events (for example, logins). See the {{site.data.keyword.appid_short}} page for more details.|
| Federation setup| Customers need to open a support case with IBMid Enterprise Federation to start the onboarding process. This is a manual process.| Customer creates an {{site.data.keyword.cloud_notm}} SAML SP configuration. This process is self-service. | Customer creates an {{site.data.keyword.appid_full_notm}} instance and configures it according to the documented steps. This process is self-service.|
| Federation maintenance (for example, certificate update)| Requires a manual interaction with the IBMid federation team.| The customer can update their {{site.data.keyword.cloud_notm}} SAML SP configuration on their own. | The customer can update their {{site.data.keyword.appid_full_notm}} instance on their own. |
| Federation scope| IBMid federation applies to every service that uses IBMid. If a customer onboards to IBMid federation, this applies to their employees when logging on to {{site.data.keyword.cloud_notm}}, but also when using other {{site.data.keyword.IBM_notm}} SaaS offerings that use IBMid.| The federation has impact only on the {{site.data.keyword.cloud_notm}} account in which the {{site.data.keyword.cloud_notm}} SAML SP is configured to allow logins. It also does not impact any other {{site.data.keyword.cloud_notm}} accounts or IBM SaaS offerings. | The federation has impact only on the {{site.data.keyword.cloud_notm}} account in which the {{site.data.keyword.appid_full_notm}} instance is configured to allow logins. It also does not impact any other {{site.data.keyword.cloud_notm}} accounts or IBM SaaS offerings.|
| Account member onboarding| Users need to be invited by their email address.| Each user that can successfully log in by using the {{site.data.keyword.cloud_notm}} SAML SP configuration will automatically be added to the {{site.data.keyword.cloud_notm}} account.| Each user that can successfully log in to the configured {{site.data.keyword.appid_full_notm}} instance will automatically be added to the {{site.data.keyword.cloud_notm}} account.|
| Cross-account membership| IBMids can be members of multiple accounts.| Users can be members of one account only. Even if multiple {{site.data.keyword.cloud_notm}} SAML SP configurations federate to the same IdP, the users are treated as separate users in each account.| Users can be members of one account only. Even if multiple {{site.data.keyword.appid_full_notm}} instances federate to the same IdP, the users are treated as separate users in each account.|
| Use of SAML assertions in access group dynamic rules| Any SAML assertion sent by the IdP can be used in access group dynamic rules.| Any SAML assertion sent by the IdP can be used in access group dynamic rules.| Any SAML assertion sent by the IdP can be used in access group dynamic rules.|
| Reliability| IBMid is a global service with a dedicated operations team. In case of an outage in a data center, IBMid can failover to a different data center.| | Any {{site.data.keyword.appid_full_notm}} instance exists in one region. Failures in that region can prevent account members from being able to log in. Users that are already logged in are usually not affected by such a failure.|
| Login behavior| Users log in by using the central login page.| You need to use a special URL to log in to your {{site.data.keyword.cloud_notm}} account. Your account administrator gets this URL from the IAM [Identity providers](/iam/identity-providers) page in the {{site.data.keyword.cloud_notm}} console.| You need to use a special URL to log in to your {{site.data.keyword.cloud_notm}} account. Your account administrator gets this URL from the IAM [Identity providers](/iam/identity-providers) page in the {{site.data.keyword.cloud_notm}} console. |
{: caption="Comparing federation through IBMid, {{site.data.keyword.cloud_notm}} SAML SP, and {{site.data.keyword.appid_full_notm}}." caption-side="bottom"}

</idp>

## Scenarios
{: #scenarios}

For additional help deciding the correct option, review the common scenarios:

<production>Using a single {{site.data.keyword.cloud_notm}} account
:   A customer is using a single {{site.data.keyword.cloud_notm}} account and no other IBM SaaS offerings.
Since the customer is not using any other {{site.data.keyword.IBM_notm}} SaaS offering or any other {{site.data.keyword.cloud_notm}} account, they have no advantage in the federation scope capabilities or cross-account capabilities of IBMid. The number of users and logins are low, so the {{site.data.keyword.appid_full_notm}} option doesn't incur costs for this account. The customer decides on {{site.data.keyword.appid_full_notm}} as the federation option.</production>
<idp>Using a single {{site.data.keyword.cloud_notm}} account
:   A customer is using a single {{site.data.keyword.cloud_notm}} account and no other IBM SaaS offerings.
Since the customer is not using any other {{site.data.keyword.IBM_notm}} SaaS offering or any other {{site.data.keyword.cloud_notm}} account, they have no advantage in the federation scope capabilities or cross-account capabilities of IBMid. The number of users and logins are low, so the {{site.data.keyword.appid_full_notm}} option doesn't incur costs for this account. The {{site.data.keyword.cloud_notm}} SAML SP is also no cost. The customer decides on the {{site.data.keyword.cloud_notm}} SAML SP as the federation option.</idp>

Using {{site.data.keyword.cloud_notm}} and other {{site.data.keyword.IBM_notm}} SaaS offerings
:   A customer is using {{site.data.keyword.cloud_notm}} and other IBM SaaS offerings.
{{site.data.keyword.IBM_notm}} has a long-lasting and strong relationship with many customers. Those customers typically consume multiple {{site.data.keyword.IBM_notm}} SaaS offerings, which require all users to use IBMid user accounts to work with those {{site.data.keyword.IBM_notm}} SaaS offerings. In that case, all customer employees would have an advantage in using IBMid federation instead of federation based on {{site.data.keyword.appid_full_notm}}. The IBMid federation gives all employees the ability to use {{site.data.keyword.IBM_notm}} SaaS offerings and the {{site.data.keyword.cloud_notm}} console by using your Identity Provider's password management and validation.

## Resources
{: #resources-federation}

The following links help you implement the federation that you choose:

[IBMid Enterprise Federation Adoption Guide](https://www.ibm.com/docs/en/ief){: external}.
:   The publicly available IBMid federation guide gives you an overview about the steps that are required to federate your Identity Provider and whom to contact to get the federation implemented. Be aware that you need an "IBM Sponsor" (for example, an {{site.data.keyword.IBM_notm}} employee that works as main contact between you and the IBMid team).

[{{site.data.keyword.cloud_notm}} Self-Service Federation for External Identity Providers](/docs/iam?topic=iam-ibm-idp-integration).
:   Documentation for the {{site.data.keyword.cloud_notm}} IAM feature to federate with an Identity Provider through SAML using {{site.data.keyword.appid_full_notm}}.

[Enabling authentication from an external identity provider](/docs/iam?topic=iam-ibm-idp-integration)
:   Follow the steps necessary to integrate your IdP with the {{site.data.keyword.cloud_notm}} SAML SP so that your users can use your {{site.data.keyword.Bluemix_notm}} account without creating IBMids. Review the section [Mapping IdP assertions to IAM claims](/docs/iam?topic=iam-ibm-idp-integration#assertion-mapping) to make sure that your users are correctly onboarded and displayed inside your {{site.data.keyword.Bluemix_notm}} account.

[Control access to cloud resources](https://developer.ibm.com/articles/identity-and-access-management-what-developers-need-to-know/){: external}.
:   This tutorial describes how to use Dynamic Rules in Access Groups so that you automate permission assignments based on attributes that your Identity Provider is sending to {{site.data.keyword.cloud_notm}} via SAML. The tutorial itself was written for IBMid federation, but the same concept and steps also work with {{site.data.keyword.appid_full_notm}} based federation.

[Using {{site.data.keyword.appid_short}} instances to build dynamic rules in access groups](/docs/iam?topic=iam-ibm-idp-integration#app-id-dynamic-rules)
:   In case you plan to use dynamic rule with {{site.data.keyword.appid_full_notm}}-based federation, make sure to use the correct syntax for the "Identity Provider" setting inside the Dynamic Rule. The section in the link is describing how to build the correct "Identity Provider" identifier.[Using IdP data to build dynamic rules in access groups](/docs/iam?topic=iam-ibm-idp-integration#app-id-dynamic-rules)
:   In case you plan to use dynamic rule with federation through {{site.data.keyword.appid_full_notm}} or the {{site.data.keyword.cloud_notm}} SAML SP, reviw this section to make sure to use the correct syntax for the "Identity Provider" setting inside the dynamic rule.

[{{site.data.keyword.cloud_notm}} Account Single Sign-on by using {{site.data.keyword.appid_full_notm}} and Microsoft Azure AD](https://medium.com/@vrvignesh/ibm-cloud-account-single-sign-on-using-ibm-cloud-app-id-and-microsoft-azure-ad-88932a5660a2){: external}
:   This blog entry shows the whole process of integrating Microsoft Azure Active Directory with {{site.data.keyword.cloud_notm}} using {{site.data.keyword.appid_full_notm}}.
Check out the documentation to learn more about Identity and Access Management in {{site.data.keyword.cloud_notm}}.
