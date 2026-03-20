---
copyright:

  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: identity provider, IdP, App ID, IAM, integration, IdP SSO, third-party authentication, dynamic rules, external identity provider, single sign on

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Enabling authentication from an external identity provider
{: #ibm-idp-integration}

You can integrate with your external identity provider (IdP) to securely authenticate external users to your {{site.data.keyword.cloud}} account. By using your IdP, you can provide a way for users in your company to use single sign-on (SSO). You can connect your cloud account to an external IdP by using the {{site.data.keyword.cloud_notm}} SAML service provider (SP), {{site.data.keyword.appid_short}}, or by federating your users to all {{site.data.keyword.IBM_notm}} products with IBMid.
{: shortdesc}

For more information about federating with {{site.data.keyword.appid_short}} and IBMid, see the [IBM Cloud SAML Federation Guide](https://www.ibm.com/products/tutorials/ibm-cloud-saml-federation-guide){: external}.
{: note}

Avoid sending {{site.data.keyword.cloud_notm}} invites for federated users because manual invitations use only IBMid. Mixing IBMid users with users who are automatically onboarded from your external IdP can cause confusion.

- IBMid users log in through the {{site.data.keyword.cloud_notm}} website.
- External IdP users must log in with a special URL.

This mismatch can lead to duplicate usernames, which might cause issues with {{site.data.keyword.containershort}}. For a smoother experience, use only your external IdP for user onboarding.

The {{site.data.keyword.containerlong_notm}} up to release 1.18 relies on unique usernames in an account. To work correctly, you must make sure that all usernames are unique across all IdPs. Make sure that the usernames that are onboarded to your account from IBMid and users that are onboarded to your account through an IAM IdP don't overlap. Otherwise, the {{site.data.keyword.containerlong_notm}} RBAC rules might get confused and give incorrect permissions.
{: note}

## Federating with the {{site.data.keyword.cloud_notm}} SAML service provider (SP)
{: #federate-cloud-saml}

Connecting your external IdP to your {{site.data.keyword.cloud_notm}} account simplifies the log-in process to your cloud account for users in your enterprise. After the integration is complete, you must provide your users with a custom URL that they use to log in each time. You don't need to invite anyone to your account. If they exist as a user in your connected IdP's user repository, they can log in with their credentials through the custom URL.

When a user authenticates successfully, the user is automatically added to the account. Added users don't get any access policies assigned by default. However, by using [dynamic rules](/docs/account?topic=account-rules) for access groups or trusted profiles, you can set up access policies that are automatically assigned based on user claims.

### Enabling and connecting your identity provider with the {{site.data.keyword.cloud_notm}} SAML SP
{: #cloud-sp-idp}

If you don't have any IAM IdP references before in your account, you must enable the login setting for your account first.

1. Enable the login settings for your account.
   1. Go to **Manage** > **Access (IAM)** > **Identity providers** in the {{site.data.keyword.cloud_notm}} console, and click **Enable**.
   2. Enter an alias for the default account URL, which you provide to users to log in to your account.

   Since you're sharing the URL with external users, make sure that the alias is unique and simple. A common format might be to use your company name or a variation of it.
   {: tip}

1. Click **Add** to add your IdP reference.
   1. Select the **{{site.data.keyword.cloud_notm}} SAML** SP.
1. Give your SP configuration a name to help distinguish it from other SP configurations that you might create to connect to other IdPs.
1. Review the advanced settings and adjust the default selections if necessary.

   Most IdPs support signed assertions, which is enough for authentication. Full response signing is often redundant if signed assertions are already enabled because the critical data, like user identity, is still protected. However, some organizations require full response signing for compliance or security policies to help ensure that every part of the message is validated.
   {: tip}

1. Download the SP configuration. Click **Next**.
1. Go to your IdP and create a new SAML 2.0 application.
1. Upload the {{site.data.keyword.cloud_notm}} SAML SP configuration and download the IdP metadata.
1. Upload the IdP metadata to {{site.data.keyword.cloud_notm}}.
1. Review the advanced settings. When you request signed SAML requests from {{site.data.keyword.cloud_notm}}, {{site.data.keyword.cloud_notm}} signs authentication requests before it sends them to your IdP. Click **Next**.
1. Click **Verify** to test the SAML connection between the {{site.data.keyword.cloud_notm}} SP and your IdP.
   1. Enter your IdP credentials, like a username and password.
1. View the results of the connection.
   - If the connection **Failed**, make sure that your IdP metadata is correct and that {{site.data.keyword.cloud_notm}} can reach your IdP. Check your IdP logs to troubleshoot SAML connection issues. Make necessary updates to the IdP or SP configuration.

      Logs might include details about authentication requests, SAML responses, and errors related to metadata mismatches or signature validation.
      {: tip}

   - If the connection **Succeeded**, click **Next**.
1. Review the IdP assertions that are automatically mapped to required IAM claims. You can override a default mapping or manually enter an attribute name from your IdP if it doesn't automatically populate. For more information, see [Mapping IdP assertions to IAM claims](/docs/account?topic=account-ibm-idp-integration#assertion-mapping).
   1. Click **Add mapping** if you want to rename a nonrequired attribute from your IdP.
1. Click **Next** and then click **Test** to test the assertion mapping.
1. Click **Finish**.

### Mapping IdP assertions to IAM claims
{: #assertion-mapping}

Manually mapping identity assertions from your IdP to {{site.data.keyword.cloud_notm}} IAM claims is optional. {{site.data.keyword.cloud_notm}} automatically maps a list of recognized IdP assertions to the required IAM claims in Table 1. If the required SAML assertion mappings are not found and no attribute mapping is available, the SAML test fails. If a required claim doesn’t map to an IdP assertion automatically, define a mapping or update the assertion name in your IdP to match the expected IAM claim.

Your IdP might send more attributes that {{site.data.keyword.cloud_notm}} doesn't require, like `region` or `department`. {{site.data.keyword.cloud_notm}} receives these additional attributes and makes them available as user claims that you can use for attribute-based access control (ABAC).

Most users don't need to create mappings, unless inconsistencies exist in your IdP configuration. For example, if your IdP uses `user_email` instead of `email`.

Complete the attribute mapping only if your IdP doesn't match the following SAML assertion schema:

| Attribute          | Source             | Description      |
|--------------------|--------------------|------------------|
| email (required) | Mapped from SAML assertion "email". | The user's email address. This is a mandatory field for authentication. |
| username (required) | Mapped from SAML assertion "preferred_username", "username", "user_name", or "userName". Falls back to "subject" if none are available. | The identifier that displays in the CLI, APIs, or other platform services. Often an email but can be another unique value. |
| firstname (required) | Mapped from SAML assertion "given_name", "givenname", "givenName", "first_name", "firstname", or "firstName". | The first name of the user that logs in. |
| lastname (required) | Mapped from SAML assertion "family_name", "familyname", "familyName", "last_name", "lastname", or "lastName". | The last name of the user that logs in. |
| Extra attributes (optional) | Custom SAML assertions provided by the IdP. | These attributes can be used in dynamic rules for access groups and trust relationships for federated users in trusted profiles. |
{: caption="List of required IAM claims and the cooresponding IdP assertions that {{site.data.keyword.cloud_notm}} recognizes." caption-side="bottom"}

## Federating with {{site.data.keyword.appid_short}}
{: #federate-appid}

If you use an external IdP reference through {{site.data.keyword.appid_short}}, each account can have up to five IdP references added through the Identity providers page in the Access (IAM) section of the console. You set up your IdP reference by selecting which {{site.data.keyword.appid_short}} instance to integrate with IAM. Then, the IdP reference is given as a random realm ID that is the unique prefix for users of that {{site.data.keyword.appid_short}} service instance.

Setting up the integration between your {{site.data.keyword.appid_short}} instance, which is already configured with your IdP, you can continue to manage all users externally in your IdP. It also simplifies the log-in process to your cloud account for users in your enterprise. After the integration is complete, you must provide your users with a custom URL that they use to log in each time. You don't need to invite anyone to your account. If they exist as a user in your connected IdP's user repository, they can log in with their credentials through the custom URL.

Review the following requirements to get started:

* Create an instance of {{site.data.keyword.appid_short}} from the {{site.data.keyword.cloud_notm}} catalog. For more information, see the [Getting started tutorial](/docs/appid?topic=appid-getting-started).
* Configure your {{site.data.keyword.appid_short}} instance. For more information about how to do this depending on your use case, see the {{site.data.keyword.appid_short}} documentation about [managing authentication](/docs/appid?topic=appid-managing-idp).
* Make sure that you have the required access to view and manage IdP references, if you aren't the account owner. Be assigned the operator role or higher on the {{site.data.keyword.appid_short}} instance and the operator or administration role on the [IAM Identity Service](/docs/account?topic=account-account-services#identity-service-account-management).

### Configuring your {{site.data.keyword.appid_short}} instance for IAM integration
{: #configure-appid-instance}

Review the following requirements about how your {{site.data.keyword.appid_short}} instance must be configured to work properly as an IAM identity provider (IdP) for your {{site.data.keyword.cloud_notm}} account.

If you plan to use your {{site.data.keyword.appid_short}} instance for IAM IdP integration, then any user can log in to your account who can authenticate with that {{site.data.keyword.appid_short}} instance. Therefore, consider the following guidelines when you configure your instance:

Disable the following types of authentication:

* Facebook
* Google
* IBMid
* Anonymous

If you use Cloud Directory as an authentication method, disable the option for users to sign up through the app, and instead add only known users individually to your [Cloud Directory](/docs/appid?topic=appid-cloud-directory).
{: tip}

#### Setting IAM-specific attributes in {{site.data.keyword.appid_short}} tokens
{: #iam-idp-attributes}

For IAM to work correctly with your external IdP, you must make sure that the {{site.data.keyword.appid_short}} instance provides all required attributes. See the following table for the required attributes:

| Attribute          | {{site.data.keyword.appid_short}} ID Token Claim            | Source             | Description      |
|--------------------|------------------------------------------------------|--------------------------|-------------------|
| identifier (required)   | ID        | {{site.data.keyword.appid_short}} generated     | A unique identifier that identifies a user. It can't be changed during the life time of that user. {{site.data.keyword.appid_short}} creates this identifier. |
| email (required)        | email    | Mapped from SAML assertion "email", which is mandatory for Cloud Directory and SAML configurations. | The user's email address. |
| username (recommended)  | preferred_username if present, otherwise sub    | Mapped from SAML assertion "preferred_username", "username", "user_name" or "userName" if available. Otherwise, the {{site.data.keyword.appid_short}} generated "sub" claim is used | When you work with the CLI, APIs, or the {{site.data.keyword.containerlong_notm}}, the username displays. A username is often an email address, but can also be a different value. If the username is not provided by {{site.data.keyword.appid_short}}, IAM uses the identifier instead. |
| firstname (recommended) | given_name if available, otherwise "notset" as default  | Mapped from SAML assertion "given_name", "givenname", "givenName", "first_name", "firstname" or "firstName" if available, otherwise IAM uses the constant "notset" | The first name of the user that logs in. |
| lastname (recommended)  | family_name if available, otherwise "notset" as default | Mapped from SAML assertion "family_name", "familyname", "familyName", "last_name", "lastname" or "lastName" if available, otherwise IAM uses the constant "notset" | The last name of the user that logs in. |
| name (optional)         | name if present, otherwise built by the firstname, a space, and the last name | No automatic mapping from SAML | Full name, including middle initial, title, or anything that is not covered by first name and last name |
{: caption="Required attributes for App ID tokens" caption-side="bottom"}

When a user authenticates successfully by using the {{site.data.keyword.appid_short}} service instance in the {{site.data.keyword.cloud_notm}} account, the user is automatically added to the account. Added users don't get any access policies assigned by default. However, by using [access groups](/docs/account?topic=account-groups) and [dynamic rules](/docs/account?topic=account-rules), you can set up automatically assigned access policies.

### Enabling and connecting your identity provider with {{site.data.keyword.appid_short}}
{: #idp-console}

If you have no IAM IdP references in your account, you must enable the login setting for your account first.

1. Enable the login settings for your account.
   1. Go to **Manage** > **Access (IAM)** > **Identity providers** in the {{site.data.keyword.cloud_notm}} console, and click **Enable**.
   2. Enter an alias for the default account URL, which you provide to users to log in to your account.

   Since you're sharing the URL with external users, make sure that the alias is unique and simple. A common format might be to use your company name or a variation of it.
   {: tip}

1. Click **Add** to add your IdP reference.
   1. Select {{site.data.keyword.appid_short}}.
1. Enter a name for the IdP reference, and select the {{site.data.keyword.appid_short}} instance that you want to connect.
1. Select how you want to onboard users:
   * **Static**: (Default) Add each user to your account when they log in the first time.
   * **Dynamic**: Add users to your account only if they log in and don't select a trusted profile.
   * **Never**: Users aren't added to your account but can access your account by using trusted profiles. For more information about trusted profiles, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).

   Say that you have onboarding set to Static and the user selects a trusted profile when they log in the first time. In this case, the user is still added to the account.
   {: note}

1. Then, select the following settings (Optional):
   * **Enable for account login?**: Enable your IdP references to be used for users to log in to your account. This option is set by default when you first create an IdP reference.
   * **Set as the default?**: Users can use the default IdP reference URL that you created when you enabled this feature to log in to your account. You can have only one default IdP reference. For all other IdP references that you create, users must use the realm IDs to log in.
1. Click **Create**.

Your IdP reference is now available on the Identity providers list and the realm ID is generated automatically as the value that represents your IAM IdP in {{site.data.keyword.cloud_notm}}.
{: note}

## Federating with IBMid
{: #federate-ibmid}

A commonly used authentication method in {{site.data.keyword.cloud_notm}} that federates you for all {{site.data.keyword.IBM_notm}} products and has no usage charges is IBMid federation by registering your company's domain. Registering a company's domain with {{site.data.keyword.IBM_notm}} enables users to log in to {{site.data.keyword.IBM_notm}} products and services by using their existing company user credentials. Your company's IdP handles authentication through single sign-on (SSO). For information about how to register your company for a federated ID, see the [IBMid Enterprise Federation Adoption Guide](https://www.ibm.com/docs/en/ief){: external}. An {{site.data.keyword.IBM_notm}} sponsor, such as a product advocate or client advocate, is required when you request to register federated IDs.

To begin setting up IBMid for enterprise federation, open a case at ibm.com/mysupport and select IBMid Enterprise Federation as the product.
{: note}

## Logging in with external identity provider credentials
{: #log-in-external-idp}

After your {{site.data.keyword.appid_short}} instance is connected to your IdP, and your {{site.data.keyword.appid_short}} instance is integrated with IAM, your users can start logging in to your account. If the IdP reference is set as the default, then you can share the **Default IdP URL** for your account.

- You can have only one set as the default, but you can have up to five set up in your account.
- Copy the **IdP URL** link from the table for the row of the IdP reference you need a URL to give to users to log in.

## Using IdP data to build dynamic rules in access groups
{: #app-id-dynamic-rules}

In addition to the required attributes, you can pass any type of information with your SAML assertion. These attributes are available for you to use in [dynamic rules in access groups](/docs/account?topic=account-rules).

To successfully build a dynamic rule, the following information is required:

Identity provider
:    For the {{site.data.keyword.cloud_notm}} SAML provider, use the Entity ID of the service provider that is configured in your IdP. For {{site.data.keyword.appid_short}}, use the prefix `appid://` and the realm ID from the IAM IdP. For example, `appid://A1B2C3D4` if the realm ID of the user was `A1B2C3D4`.

Add users when
:   Use the name of the additional SAML assertion. This property is passed through unchanged.

You can use custom attributes in dynamic rules, too. However, if you have the same property as a custom attribute and as a SAML assertion, then the custom attribute from the SAML assertion is used.

If you are working with an external IdP, connect with one external IdP only, and have users onboard automatically through this IdP.

## Using IdP data to build trusted profiles
{: #trusted-profiles-idp-data}

After you enable and connect your IdP, you can start [creating trusted profiles](/docs/account?topic=account-create-trusted-profile). To build trust with federated users, you can use the personal data from your IdP to search attribute names and values that exist in your organization.

If the users that you are creating a trusted profile for use {{site.data.keyword.appid_full_notm}}, create the trusted profile as an App ID user, and likewise for IBMid. This way, your own SAML attributes can give you an idea of how to structure the trusted profile conditions. Other users with the same IdP can have different SAML attributes and you can use your own only as a hint. To use attributes in a claim that are different than your own, input them manually.
{: tip}

The conditions that you create filter out or allow federated users to apply the trusted profile. Access depends on which attributes the federated users are assigned in your corporate user directory. When you create a trusted profile, you can view IdP data to see your own user claims from your organizations corporate user directory.

Say an attribute that is called `groups` identifies departments, teams, and more granular internal organizations within your company. If developers in the US on the finance team need as much access for a project, you might create a trusted profile with the following conditions:

* Allow users when `groups` equals `finance-dev`
* Allow users when `country` equals `us`

To make sure that your conditions allow only the federated users you intend to grant access to, contact your corporate directory architect for more information on available attributes.

For more information about the fields that are used to create conditions, see [IAM condition properties](/docs/iam?topic=iam-condition-properties).

Create narrow conditions. You share an IdP URL with everyone in your organization. If a claim rule is too open, you might allow users to apply a trusted profile with access to your account unintentionally.
{: important}
