---

copyright:

  years: 2017, 2026
lastupdated: "2026-08-28"

keywords: trusted profiles, federated users, compute resources, identity provider, SSO, single sign-on, workload identity, enterprise templates, centralized management, least-privilege access, Power Virtual Server, PowerVS

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Trusted profiles overview
{: #trusted-profiles-overview}
{: support}
{: help}

Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory. Trusted profiles can also be used to set up fine-grained authorization for applications that are running in compute resources. This way, you aren't required to create service IDs or API keys for the compute resources.
{: shortdesc}

Assign access to the profile by adding it to an access group or by assigning individual policies, and then add or remove conditions as needed to grant or deny access to account resources. By using trusted profiles, you can centrally manage the access lifecycle to multiple {{site.data.keyword.cloud_notm}} assets. For more information, see [Creating trusted profiles](/docs/iam?topic=iam-create-trusted-profile).

## Federated users
{: #trusted-profiles-feature-fedusers}

Your users might already have identities outside of {{site.data.keyword.cloud_notm}} in your corporate directory. If your users need to work with {{site.data.keyword.cloud_notm}} resources or work with applications that access those resources, then those users also need {{site.data.keyword.cloud_notm}} credentials. You can use a trusted profile to specify permissions for users whose identity is federated from your organization or an external identity provider (IdP). By using your identity provider, you can provide a way for users in your company to use single sign-on (SSO). To connect your federated users with {{site.data.keyword.cloud_notm}} resources, see [Federating users to {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-identity-overview#users-bestpract).

![Introducing IBM Cloud trusted profiles](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_y9tupkqk){: video output="iframe" data-script="#video-transcript-tp" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

### Video transcript
{: #video-transcript-tp}
{: notoc}

We are excited to introduce the latest and greatest identity type: IBM Cloud trusted profiles. You expect the most reliable and efficient way to manage access to your account, so let's learn about how you can use trusted profiles.

Previously, organizing identities and assigning access was limited to access groups, where each user is added to the account manually.

As an account owner, you can save time and automatically grant federated users access to your accounts by leveraging the attributes that already exist in your corporate directory.

Simply add conditions based on SAML attributes to define which federated users can apply a profile. This way, changes in your directory immediately affect access to resources.

As a federated user, you might have the option to apply one of many trusted profiles. After you log in, you can apply a profile, or continue to the console.

Imagine a scenario where you want to complete developer-related tasks, like working with the service instances from your application components. You can select the Developer profile when logging in to ensure that you have the access you need.

Similarly, if you want to complete an administrator-related task, you can select the Admin profile that has privileged permissions. This way, you reduce the risk of taking privileged actions by mistake.

You also have the option to log in to the account without applying a profile by continuing to the console.

To learn more about how trusted profiles work check out our IBM Cloud Identity and Access Management documentation which includes tutorials and other helpful resources to get started!

### Selecting a trusted profile
{: #selecting-profile}

After authenticating, federated users are presented with the profile selection page, which lists all trusted profiles available to them across accounts. The interface is designed to scale efficiently, making it easy to find the right profile even when you have access to many profiles across multiple accounts.

**Multiple view options**
:   Toggle between Grid view (detailed tiles showing profile name, account, description, type, and session duration) and List view (table format for scanning large lists).

**Powerful search**
:   Find profiles by trusted profile name, account name, or description using full-text search.

**Flexible filtering**
:   Filter by account, profile type (Individual or Federated), or pinned profiles.

**Pin favorites**
:   Mark frequently used profiles for quick access so they appear at the top of the list.

**Continue without a profile**
:   Choose to access the account with base permissions (access group memberships and individual policies) only, without applying a trusted profile.

For more information, see [Understanding the profile selection experience](/docs/iam?topic=iam-create-trusted-profile#profile-selection-experience).

### Switching between profiles
{: #switching-profiles}

After logging in, federated users can switch between available trusted profiles without logging out by using the profile switcher in the console header (upper right corner). From the profile switcher, you can:

- View your current profile or user identity and the account you are accessing
- Switch to other available trusted profiles in the current account
- Switch back to your own user identity without logging out
- Access profile details and CLI login information

## Compute resources
{: #trusted-profiles-feature-resources}

By using trusted profiles, you can define fine-grained authorization for all applications that are running in a compute resource without creating service IDs or managing the API key lifecycle for applications. The trusted profiles provide better control for granting access to compute resources. This includes {{site.data.keyword.powerSys_notm}} instances, which can use instance identity tokens from the metadata service to authenticate with trusted profiles.

* Application developers can programmatically retrieve a token that is associated with the compute resource identity that they are running on. That token is used to get the trusted profile identity token, which is used to access services and resources on {{site.data.keyword.cloud_notm}}. For {{site.data.keyword.powerSys_notm}}, applications retrieve instance identity tokens from the metadata service at `https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token` and exchange them for IAM tokens through the same service.
* Applications running on a compute resource can have a flexible, but secure way to access other {{site.data.keyword.cloud_notm}} services from within compute resources. For example, it's more secure not having to store API keys. SAP workloads running on {{site.data.keyword.powerSys_notm}} can securely access {{site.data.keyword.cos_full_notm}} for backups without embedding credentials by using trusted profiles with conditions based on instance attributes like workspace, region, or resource group.
* All compute resource instances that share certain conditions such as name, namespace, tags, or location, their identities are mapped to a common profile and can share access to {{site.data.keyword.cloud_notm}} resources. This common identity makes it possible to give the applications within various compute resources access to an external resource one time rather than cluster-by-cluster.

## Centrally managing access in enterprises
{: #enterprise-templates-feature}

Your enterprise can easily scale access management and ensure consistent account security settings throughout the organization by using enterprise-managed IAM templates. You can create templates for IAM resources like access groups, trusted profiles, and account security settings that you assign throughout the enterprise. When you assign an IAM template to child accounts, enterprise-managed IAM resources are created in the child accounts you select.

For example, there might be a certain job role in every child account that requires the same permissions. You can create an access group template with the necessary access policies and assign the template to all of the child accounts in your enterprise. This approach enables centralized management of workload access while reducing policy drift and ensuring that users with that job role have only the least-privilege access that is necessary in each account.

For more information, see [How enterprise-managed IAM works](/docs/enterprise-management?topic=enterprise-management-access-enterprises#how-enterprise-iam).

## Next steps
{: #trusted-profiles-next-steps}

* [Create a trusted profile for federated users](/docs/iam?topic=iam-create-trusted-profile&interface=ui).
* [Create a trusted profile for compute resources](/docs/iam?topic=iam-trustedprofile-compute-tutorial).
* Learn about [authentication features](/docs/iam?topic=iam-types).
