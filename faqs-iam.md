---

copyright:

  years: 2018, 2026
lastupdated: "2026-05-06"

keywords: frequently asked questions, iam faqs, administrator, administrator role

subcollection: iam

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about IAM
{: #iamfaq}

FAQ for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) might include questions about access control for resources, resource groups, account management, classic infrastructure resources, and access groups.
{: shortdesc}

To find all FAQ for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).

## What is {{site.data.keyword.cloud_notm}} Identity and Access Management?
{: #whatisiam}
{: faq}
{: support}

Identity and Access Management (IAM) enables you to securely authenticate users for platform services and control access to resources across the {{site.data.keyword.cloud_notm}} platform. A set of IBM Cloud services is enabled to use Cloud IAM for access control. They are organized into resource groups within your account to enable giving users quick and easy access to more than one resource at a time. Cloud IAM access policies are used to assign users, service IDs, and trusted profiles access to the resources within your account. For more information, see [{{site.data.keyword.cloud_notm}} Identity and Access Management](/docs/iam?topic=iam-iamoverview).

## What is an IAM-enabled service?
{: #iam-enabled}
{: faq}

An IAM-enabled service must be in a resource group and access to the service is given by using IAM access policies. When you create an IAM-enabled service from the catalog, you must assign it to a resource group. For more information, see [Managing resources](/docs/account?topic=account-manage_resource)

{{site.data.keyword.containerlong_notm}} is the only exception; it’s IAM-access controlled, but is always assigned to the default resource group. Therefore, you aren’t given the option to choose one when you create it from the catalog. And, it can’t be assigned to any other resource group.

## What is an IAM access policy?
{: #iam-policies}
{: faq}

An IAM access policy is how users, services IDs, trusted profiles, and access groups in an account are given permission to work with a specific IAM-enabled service or resource instance, manage a resource group, or complete account management tasks. Each IAM access policy is made of a subject, target, and role. A subject is the who that has the access. The target is what the subject can have access to. And, the role, whether it is a platform or service role depending on the context of the selected target, defines what level of access the subject has on the target.

A subject is a user, service ID, trusted profile, or access group. A target can be a service in the account, a resource group in the account, a specific resource instance or type, or an account management service. And, the roles that are provided as choices depend on your selected target. Some services have service-specific roles that are defined, and some use platform roles only. To understand this concept visually, check out the following graphic with an outline of the options for creating an IAM policy:

![Creating IAM policies](images/IAM.svg "How IAM access policies are created by using a subject, target, and role"){: caption="How IAM access policies are created by using a subject, target, and role" caption-side="bottom"}

## How do I find out what I have access to?
{: #iam-access}
{: faq}
{: support}

In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select your name on the Users page. Then, depending on the access you're looking for, open the different tabs:

* To determine what access you have through the access groups you are assigned, select **Access** and view the Access groups table.
* To see IAM access policies that are assigned to you, select **Access** and view the Access policies table.

## What actions are mapped to each IAM role?
{: #action-mapping}
{: faq}

When you invite a new user or assign a user IAM access, you can view the actions that are associated with each role. Click the numbers listed next to each role to view a list of all actions that are mapped to a specific role. By reviewing the mapping of actions to roles, you can confidently know what access you're assigning.

## How do I request access to a resource?
{: #request-access}
{: faq}

The account owner can update your access to any resource in the account, or you can contact any user who is assigned the administrator role on the service or service instance.

## How do I find the IAM ID for a user or myself?
{: #iam-id}
{: faq}

In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Users**. Then, select your name or another user's name from the list. You can find the IAM ID for that user along with their email address on the User details page.

## How do I identify platform management roles and service access roles for a user?
{: #iam-role}
{: faq}

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and then select **Users**.
2. Select your name or another user's name from the list.
3. Click **Access** to view the permissions that are associated with the user.

The `owner` tag is listed for the owner of the account. This user is assigned the administrator role on the service or service instance.
{: note}

## How do I find and manage API Keys for a user or myself?
{: #iam-api-keys}
{: faq}
{: support}

In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys** to view and manage API keys that you have access to.

* For information about how to manage {{site.data.keyword.cloud_notm}} API keys that are associated with user identities, see [Managing user API keys](/docs/iam?topic=iam-userapikey).
* For information about how to manage API keys that are associated with a service ID, see [Managing service ID API keys](/docs/iam?topic=iam-serviceidapikeys).
* For information about how to manage classic infrastructure API keys, see [Managing classic infrastructure API keys](/docs/iam?topic=iam-classic_keys).

## Where do I find or add service credentials?
{: #service-credentials}
{: faq}

To view an existing service credential for a service or to add a new credential, go to your resource list by clicking the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Resource list**, then select the name of the service to open its details. Click **Service credentials** to view the details or to select **New Credential**.

To save a copy of the service credentials, most services provide a  download option or the option to copy to your clipboard.
{: note}

## Why use resource groups and access groups?
{: #resource-groups}
{: faq}

A resource group is a logical container for resources. When a resource is created, you assign it to a resource group and the resource can't be moved.

An access group is used to easily organize a set of users, service IDs, and trusted profiles into a single entity to make access assignments easy. You can assign a single policy to an access group to grant all members those permissions. If you have more than one user or service ID that needs the same access, create an access group instead of assigning the same access multiple times per individual user, service ID, or trusted profile.

By using both resource groups and access groups, you can streamline the access assignment policy by assigning a limited number of policies. You can organize all of the resources a specific group of users and service IDs needs access to in a single resource group, group all the users or service IDs into an access group, and then assign a single policy that grants access to all resources in the resource group.

For more information, see [Best practices for organizing resources and assigning access](/docs/account?topic=account-account_setup#how_access).

## How do I ensure that my users can create resources within a resource group?
{: #resources}
{: faq}
{: support}

To create a resource in a resource group, the user must have two access policies: one assigned to the resource group itself, and one assigned to the resources in the group. Access to the resource group itself is simply access to the container that organizes the resources, and this type of policy allows a user to view, edit, or manage access to the group, but not the resources within it. Access to services within the resource group enables a user to work with the service instances, which means the user can create a service instance.

So, minimally the user must have the following access:

* Viewer role or higher on the resource group itself
* Editor role or higher on the service or all services in the resource group

## How do I assign access to all resource groups?
{: #all-rgs}

To assign a user, service ID, or access group a policy on all resource groups,you must assign the following:

* A policy for **All Identity and Access enabled services** with the **Viewer** resource group access role selected. However, you must also assign at least one platform or service role to assign this type of policy.
* A policy for **All Account Management services** with the **Viewer** role or higher provides access to view all resource groups. However, be aware that this type of policy also assigns the role that you choose for each account management service, so it can be a powerful policy that enables a user to manage users, account settings, billing information, and more.
* A policy with **Resource group only** and a particular resource group that is selected as well as a resource group access role assigned. You can repeat this type of policy as needed for each available resource group in the account.

You can also assign access to individual resource groups with a policy on a service as long as you select a targeted resource group by name and assign a resource group access role.
{: tip}

## What access enables a user to work with a single resource?
{: #resources-and-rg}
{: faq}

A user must be assigned an access policy on the specific resource with at least the Viewer role that is assigned on the resource group itself that contains the resource. To assign this type of policy, see [Assigning access to resources](/docs/iam?topic=iam-assign-access-resources).


## What access do I need to provide others access?
{: #user-access}
{: faq}
{: support}

For IAM-enabled services, you must have Administrator role on the service or resource that you want to assign users access to. If you want to assign access to all services or resources in the account, you need a policy on **All Identity and Access enabled services** with the Administrator role. And, to assign users access to account management services, you must be assigned the Administrator role on the specific service or all account management services. Assigning users the Administrator role delegates the granting and revoking of administrator access of the account, including the ability to revoke access for other users with the administrator role.

For classic infrastructure, you must have the Manage user classic infrastructure permission and the service and device category permissions for the resources that you want to give the user access to.

## What's the difference between access to manage a resource group and access to resources within a resource group?
{: #providing-access}
{: faq}

When you have access to manage a resource group, you can view, edit the name, and manage access for the resource group itself depending on the assigned role. Access to a resource group itself doesn't give a user access to the resources within the group.

When you have access to resources within a resource group, you can edit, delete, and create instances, or have all management actions for the specified services within the resource group depending on the assigned role.

For example, platform management roles and actions for account management services, see [Platform roles table](/docs/iam?topic=iam-userroles#platformroles).

## Who can remove users?
{: #remove-users}
{: faq}

The account owner can remove any users from the account, and any user with the following access can remove users from an account:

* An IAM policy for the User management account management service with the Administrator role assigned.
* If you have classic infrastructure in your account, then a user must have an IAM policy for the User management account management service with the Administrator role assigned, and be an ancestor of the user in the classic infrastructure user hierarchy with the Manage user classic infrastructure permission assigned.

## How do I require multifactor authentication for my account?
{: #multi-factor}
{: faq}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Settings**.
2. From the Authentication section, click **Edit** to select MFA for all users or non-federated users only.

For more information, see [Requiring MFA for users in your account](/docs/iam?topic=iam-enablemfa).

## What is the difference between service and platform roles?
{: #service-platform-roles}
{: faq}

Service and platform roles are two different types of roles:

* Platform roles are how you work with a service within an account such as creating instances, binding instances, and managing user's access to the service. For platform services these roles enable users to create resource groups and manage service IDs, for example. Platform roles are: administrator, editor, operator, and viewer.

* Service roles define the ability to perform actions on a service and are specific to every service such as performing API calls or accessing the UI. Service roles are: manager, writer, and reader. For more information about how these roles apply, refer to the specific service's documentation.

## How do I assign a user full access as an account administrator?
{: #account-administrator}
{: faq}
{: support}

To assign a user in your account full administrator access, go to **Manage > Access (IAM)** in the console, select the user's name, and assign the following access:

* An IAM policy with Administrator and Manager roles on All Identity and Access enabled services, which enable a user to create service instances and assign users access to all resources in the account.
* An IAM policy with Administrator role on All account management services, which enables a user to complete tasks like inviting and removing users, managing access groups, managing service IDs, managing private catalog products, and track billing and usage.

* The Super user permission set for classic infrastructure, which includes all of the available classic infrastructure permissions

* A trusted profile set as the alternative account owner has the highest level of classic infrastructure permissions and has both IAM policies that grant full access. For more information, see [Setting an alternative account owner](/docs/account?topic=account-transfer).

## Can every user in my account see all the other users?
{: #users}
{: faq}

An account owner can view all users in the account and choose how users can view other users in the account on the Users page. An account owner can adjust the [user list visibility setting](/docs/iam?topic=iam-iam-user-setting) on the Settings page by selecting one of the following options:

* **Unrestricted view**: All users in your account can view everyone else in the account.
* **Restricted view**: Limits the ability to view users on the Users page to only those who have been granted explicit access, along with those who have visibility of other users through a classic infrastructure user hierarchy relationship.

## Do I need to assign access to a user when I invite them to the account?
{: #account-invite}
{: faq}

No. You can invite users, and then assign access later.

## What does it mean for a user to be in pending state?
{: #pending-user}
{: faq}

A user who is list as `Pending` is a user who has been invited to {{site.data.keyword.cloud_notm}} but who hasn't accepted their invitation. On the Users page, the management actions for these users include resending the invitation or cancelling the invitation. 

When inspecting access group memberships or access policies in your account, you might see memberships or policies that are related to pending users that were created as part of the invite. These display with an IAM ID that uses the `BSS-`. This IAM ID is a placeholder for the memberships and policies until the user accepts the invitation. And, since the user hasn't registered with {{site.data.keyword.cloud_notm}}, they can't retrieve an IAM access token to leverage the assigned access. When the user accepts the invitation and registers with {{site.data.keyword.cloud_notm}}, the ID in these memberships and policies is replaced with their assigned IAM ID.


## How do I add authentication into my web and mobile apps?
{: #appid}
{: faq}

IAM is used to manage access to your {{site.data.keyword.cloud_notm}} services and resources. With {{site.data.keyword.appid_full_notm}}, you can take cloud security one step further by adding authentication into your web and mobile apps. With just a few lines of code, you can easily secure your Cloud-native apps and services that run on {{site.data.keyword.cloud_notm}}. Ready to get started? [Check out the docs](/docs/appid?topic=appid-getting-started#getting-started).

## Where do I manage a user's access to infrastructure?
{: #infrastructure-devices}
{: faq}
{: support}

Access for classic infrastructure starts with the user. For more information, see [Managing classic infrastructure access](/docs/iam?topic=iam-mngclassicinfra).

If you need to assign access to IAM-enabled infrastructure services, such as {{site.data.keyword.vpc_full}}, you assign access to a user by completing the following steps:

1. Click **Manage** > **Access (IAM)** > **Users**
1. Select the user.
1. Click **Access**.

## How do I manage access for users previously assigned billing and support permissions in my SoftLayer account?
{: #migrated-permissions-faq}
{: faq}
{: support}

All permissions that were previously assigned in your SoftLayer account can be managed in the {{site.data.keyword.cloud_notm}} console. Account permissions for managing billing information and support cases are now available in [managing migrated SoftLayer account permissions](/docs/iam?topic=iam-migrated_permissions). All users who were previously assigned these permissions in your SoftLayer account were migrated to these access groups, which are assigned the same level of access by using an IAM policy on the access group.

## How do I determine how many policies exist in my account?
{: #total-policies}
{: faq}

You can [viewing the total number of policies per account](/docs/iam?topic=iam-account-limits&interface=cli#total-number-policies-cli) by using the CLI to ensure that you don't exceed the limit for your account.

## What are verification methods and what they are used for?
{: #verification-methods}
{: faq}

Verification methods are used to prove your identity and access the Verification methods and authentication factors page.

The first time that you log in to your account after MFA settings are updated, you also need to verify your identity by using two different verification methods. Verification methods include email, text, or phone call, and you can use any combination of those options to verify your identity. After you verify your identity, you set up and provide details for your authentication factor on the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page.

## What are authentication factors and what are they used for?
{: #authenticaiton-factors}
{: faq}

These factors can be something that you have, like a security key, or that you receive, like a time-based one time passcode (TOTP) or OTP. If an administrator enables MFA in at least one of the accounts you are a member of, you must provide two or more factors each time you log in. If you are a member in multiple accounts and at least one of the accounts uses MFA, MFA is required each time that you log in. This applies regardless of the account that you are trying to access. For more information, see [Managing verification methods and MFA factors](/docs/iam?topic=iam-verification-authentication).

## How do I reset a verification method?
{: #reset-verification}
{: faq}

A verification method becomes inaccessible if a phone number or email address that's associated with your identity changes or you no longer have access to it. To reset a verification method, [open a support case](/unifiedsupport/cases/form) and add a verification method that you can use to access the Verification methods and authentication factors page.

## How can I get a new QR code for MFA setup?
{: #qr-code}
{: faq}

To get a new QR code for MFA setup, go to the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page. From the Authentication factors section, click **Show authentication factors** > **Add**. Next, choose a type and select **TOTP**. Then, the new QR is available. After you scan the QR code, enter the TOTP that is generated by the authenticator app to confirm your choice. Now, each time you log in you provide the TOTP generated by the authenticator app that you just set up.


## How do I change the email address that is used for MFA?
{: #method-update}
{: faq}

You can update the email address that is used for MFA on the [Verification methods and authentication factors](https://iam.cloud.ibm.com/mysecurity){: external} page. From the Authentication factors section, click **Show authentication factors** > **Add**. Select **Email-based** and enter the email address where you want to receive OTPs as an authentication factor. Then, enter the OTP you receive to confirm your choice. Next, click **Complete**. After you add the new factor, select the old email address, and click **Remove**.

## Can trusted profiles create user API keys?
{: #tp-apikey}
{: faq}

If you use a trusted profile, you can't create a user API key. You can still create and manage all other API keys. For example, service ID API keys.

To create a user API key, your IAM ID and the IAM ID of the user that's requesting the user API key must be the same. When you apply a trusted profile, you take on the IAM ID of that profile. To create a user API key for your identity, use the account switcher to switch from a trusted profile to an account where your IAM ID is a member.

## How can I check whether a user can apply a trusted profile?
{: #tp-check}
{: faq}

To check whether a user qualifies to apply a trusted profile by using the IBMid identity provider (IdP), the user and the administrator must complete specific steps.

1. The user must go to [{{site.data.keyword.cloud_notm}} User Claims](https://identity-1.us-south.iam.cloud.ibm.com/identity/claims?realm_id=IBMid){: external}.
1. From here, the claims are displayed.
1. The user must provide the claims to the administrator.
1. As the administrator, compare the claims of the user with the conditions set for the trusted profile. To view the conditions for a trusted profile, go to **Manage** > **Access (IAM)** > **Trusted profiles** in the {{site.data.keyword.cloud_notm}} console.
1. Click the profile and view the **Conditions** column.
1. If the user's claims satisfy all of the conditions, the user can apply the profile.

If you are using a different IdP, check the user's claims in your corporate directory. Then, compare the claims of the user with the conditions set for the trusted profile. If the claims and the rules match, the user can apply the profile.
{: note}

## How do I establish trust with the Kubernetes service in a trusted profile?
{: #tp-kub-trust}
{: faq}

In Kubernetes, a service account provides an identity for processes that run in a Pod, and namespaces provide a mechanism for isolating groups of resources within a single cluster. All Kubernetes clusters have a `default` namespace, and each namespace has a `default` account.

When you establish trust with the Kubernetes service in a trusted profile, you are required to enter information in the `namespace` and `service account` fields. You can enter `default` for both.

For more information, see [Using Trusted Profiles in your Kubernetes and OpenShift Clusters](https://www.ibm.com/think){: external} and [Kubernetes namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/){: external}.

## How can I view dynamic members of access groups?
{: #dynamic-members}
{: faq}

To view a list of dynamic members in an access group, go to **Manage** > **Access (IAM)** > **Access groups** in the {{site.data.keyword.cloud_notm}} console. Select an access group and click **Users**. Dynamically added users are indicated by the type `Dynamic`. For more information, see [Viewing dynamic members of access groups](/docs/iam?topic=iam-rules#view-dynamic-users)

## How do I find inactive users, service IDs, trusted profiles, and API keys in my account?
{: #unused-identities}
{: faq}

To view a list of the inactive identities in your account, go to **Manage** > **Access (IAM)** > **Inactive identities**. You might want to remove inactive identities if they are no longer needed. For more information, see [Identifying inactive identities](/docs/iam?topic=iam-id-inactive-identities).

## How do I switch between trusted profiles and accounts?
{: #switch-profile}

You can switch between trusted profiles and accounts where you are a member by using the account switcher in the console menu bar.

![A screen capture of the account switcher](images/account-profile-switcher.svg "How to switch between trusted profiles and accounts."){: caption="How to switch between trusted profiles and accounts" caption-side="bottom"}

If you aren't a member of any account, you might have to log out and log back in to select a different trusted profile. To do so, complete the following steps.

1. Go to the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Log out**.
1. To confirm, click **Log out**.
1. Go to `https://cloud.ibm.com/login` to log in again.
1. Enter your credentials and click **Continue**.
1. On the trusted profiles landing page, select a trusted profile.
