---

copyright:

  years: 2020, 2026
lastupdated: "2026-08-13"

keywords: login, how login works, login flow, login diagram, login sequence

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} login sequences
{: #login-sequence}
{{site.data.keyword.cloud_notm}} supports multiple login sequences for different authentication scenarios. This topic explains the available login options and provides detailed sequence flows for federated, non-federated, and users added through {{site.data.keyword.appid_full_notm}} with a SAML provider connected to {{site.data.keyword.cloud}} Identity and Access Management (IAM).
{: shortdesc}

The following table compares the key characteristics of each login option:
| Criteria | Non-federated IBMid | Federated IBMid | {{site.data.keyword.appid_short}} with SAML | {{site.data.keyword.cloud_notm}} SAML provider | IdP-initiated login |
|----------|---------------------|-----------------|----------------------------------------------|------------------------------------------------|---------------------|
| **Protocol** | OAuth2 | SAML 2.0 with OpenID Connect | SAML 2.0 with OpenID Connect | SAML 2.0 | SAML 2.0 |
| **Login URL** | `https://cloud.ibm.com` | `https://cloud.ibm.com` | `https://cloud.ibm.com/authorize/<account_id>` or `https://cloud.ibm.com/authorize/<account_alias>` | `https://cloud.ibm.com/authorize/<account_id>` or `https://cloud.ibm.com/authorize/<account_alias>` | Enterprise IdP portal |
| **Federation support** | No | Yes | Yes | Yes | Yes |
| **Identity provider** | IBMid | Enterprise IdP with IBMid | Enterprise IdP with {{site.data.keyword.appid_short}} | Enterprise IdP | Enterprise IdP |
| **Login initiation** | {{site.data.keyword.cloud_notm}} console | {{site.data.keyword.cloud_notm}} console | {{site.data.keyword.cloud_notm}} console | {{site.data.keyword.cloud_notm}} console | External IdP portal |
| **Account-specific URL** | No | No | Yes | Yes | No |
| **Primary use case** | Standard {{site.data.keyword.cloud_notm}} users with IBMid | Enterprise users with existing IBMid federation | External users authenticated through {{site.data.keyword.appid_short}} | External users with direct SAML integration | Users accessing {{site.data.keyword.cloud_notm}} from enterprise portal |
{: caption="Comparison of login options" caption-side="bottom"}

## Login sequence for non-federated users with an IBMid
{: #non-fed-ibmid-login}

The standard login sequence for users in {{site.data.keyword.cloud_notm}} that are not federated works according to the following sequence:

![Login process for non-federated users with an IBMid](images/login-nonfed-id.svg "Login process for non-federated users with an IBMid"){: caption="Login process for non-federated users with an IBMid" caption-side="bottom"}

1. The user starts by visiting the URL https://cloud.ibm.com with a browser. The {{site.data.keyword.cloud_notm}} console  sends back a login page to the browser.
2. On the login page, the user enters their username, clicks Continue, then enters their password and sends this information to the console by clicking Log in.
3. The username and password combination is forwarded by the console to the IAM component of {{site.data.keyword.cloud_notm}}.
4. IAM uses the IBMid system to validate if the username and password combination is correct.
5. After successful validation, IAM responds to the console with a success response and provides a URL that the console should send to the user's browser, so that the user can finish the login sequence.
6. The browser consumes the redirect instruction and navigates to IAM to allow {{site.data.keyword.cloud_notm}} to finish the login sequence. This browser redirect is necessary to set necessary single-sign-on cookies on the user's browser that prevents the user from entering the login credentials again.
7. IAM then finishes its authentication flow with the console by sending an OAuth2 compliant redirect with an authorization code to the browser.
8. The browser provides the authorization code to the console, which in turn is used to retrieve the required tokens from IAM.
9. When the console receives the tokens, the login sequence ends. The console can now invoke {{site.data.keyword.cloud_notm}} APIs and identify the user.
10. The console displays the dashboard with user-specific content.

## Login sequence for federated users with an IBMid
{: #fed-ibmid-login}

IBMid allows enterprise customers to federate their user authentication and authorization system with IBMid. This way, users don't need to manage another user ID. Instead, they are able to log in into {{site.data.keyword.cloud_notm}} using their well-known customer-managed user ID. The login sequence for federated users in {{site.data.keyword.cloud_notm}} works according to the following sequence:

![Login process for federated users with an IBMid](images/login-fed-id.svg "Login process for federated users with an IBMid"){: caption="Login process for federated users with an IBMid" caption-side="bottom"}

1. The user starts by visiting the URL https://cloud.ibm.com with a browser. The {{site.data.keyword.cloud_notm}} console sends back a login page to the browser.
2. On the login page, the user enters their username.
3. After clicking to continue, the {{site.data.keyword.cloud_notm}} console redirects the user's browser to {{site.data.keyword.cloud_notm}}'s IAM component. As part of the redirect, the already entered username is transmitted.
4. With the help of the username, IAM is able to determine the identity provider (IdP) that should be used to run the login sequence. Therefore, IAM is sending back a redirect request to the user's browser.
5. The browser is completing the redirect and displays the enterprise customer's login page. For this interaction, a SAML request is sent to the enterprise customer's user authentication and authorization system.
6. After validating the user's credentials, the enterprise customer's system sends a redirect instruction to the user's browser. Part of this redirect is the SAML response containing assertions that describe the user and the additional attributes of that user.
7. The browser completes the redirect and sends the SAML response with assertions to IBMid.
8. IBMid validates the SAML response and maps the user to an IBMid.
9. IBMid sends a redirect to the user's browser with an authorization code to continue the authentication flow according to the OpenID Connect standard.
10. The browser contacts IAM and provides the authorization code, so that IAM can retrieve the required tokens from IBMid using the OpenID Connect standard.
11. After IBMid provides the required tokens, IAM is now finishing its authentication flow with the console by sending an OAuth2 compliant redirect with an authorization code to the browser.
12. The browser provides the authorization code to the console, which in turn is used to retrieve the required tokens from IAM.
13. When the console receives the tokens, the login sequence ends. The console can now invoke {{site.data.keyword.cloud_notm}} APIs and identify the user.
14. The console displays the dashboard with user-specific content.

## Login sequence for {{site.data.keyword.appid_short}} with a connected SAML partner
{: #appid-saml-login}

If you choose to integrate with your external IdP to securely authenticate external users to your account by using an {{site.data.keyword.appid_short}} instance, the login sequence works according to the following sequence. For more information about this type of authentication, see [Enabling authentication from an external identity provider](/docs/iam?topic=iam-ibm-idp-integration).

![Login process for users who are connected from an App ID instance connected with a SAML partner](images/login-appid-saml-new.svg "Login process for users who are connected from an App ID instance connected with a SAML partner"){: caption="Login process for users who are connected from an App ID instance connected with a SAML partner" caption-side="bottom"}

1. The user starts by going to an account-specific URL with their browser. This is either `https://cloud.ibm.com/authorize/<account id>` or `https://cloud.ibm.com/authorize/<account alias>`. The account alias can be configured on the IAM Identity Provider configuration pages in the {{site.data.keyword.cloud_notm}} console.

   Using a specific URL is required to address the correct federated SAML partner.
   {: note}

2. The {{site.data.keyword.cloud_notm}} console redirects the user's browser to {{site.data.keyword.cloud_notm}}'s IAM component. As part of the redirect, the account ID or alias is sent to IAM, and IAM detects that authorization is required for the user.

3. With the help of the account ID or alias, IAM checks the account federation configuration and determines the {{site.data.keyword.appid_short}} instance that is needed to run the login sequence. Therefore, IAM sends back a redirect request to the user's browser.

4. The browser completes the redirect and ends on an {{site.data.keyword.appid_short}} provided page. This page immediately returns a redirect to the browser containing a SAML request. The SAML request is sent to the enterprise customer's user authentication and authorization system.

5. The user enters their credentials on the enterprise customer's authentication page. The enterprise customer's system verifies these credentials and sends a redirect instruction to the user's browser. Part of this redirect is the SAML response containing assertions that describe the user and the additional attributes of that user.

6. The browser completes the redirect and sends the SAML response with assertions to the {{site.data.keyword.appid_short}} instance. After validating the SAML response, {{site.data.keyword.appid_short}} creates an authorization code and sends a redirect to the browser according to the OpenID Connect standard.

7. The browser contacts IAM and provides the authorization code. IAM then exchanges this code for access tokens with {{site.data.keyword.appid_short}} according to the OpenID Connect standard.

   Access tokens are exchanged directly between IAM and {{site.data.keyword.appid_short}} servers and never pass through the browser.
   {: tip}

8. After {{site.data.keyword.appid_short}} provides the required tokens to IAM, IAM finishes its authentication flow with the console by sending an OAuth2 compliant redirect with an authorization code to the browser. The browser provides this authorization code to the console, which then retrieves the required tokens from IAM.

   OAuth2 tokens are exchanged directly between the console and IAM servers, to maintain security throughout the flow.
   {: tip}

9. After the console receives the tokens, it can use {{site.data.keyword.cloud_notm}} APIs and identify the user. The user is logged in and the dashboard with user-specific content is displayed.

## Login sequence for {{site.data.keyword.cloud_notm}} SAML service provider
{: #ibmcloud-saml-login}

If you choose to integrate with your external IdP to securely authenticate external users to your account by using the {{site.data.keyword.cloud_notm}} SAML service provider, the login sequence works according to the following sequence. For more information about this type of authentication, see [Enabling authentication from an external identity provider](/docs/iam?topic=iam-ibm-idp-integration).

![Login process for users who are connected from the {{site.data.keyword.cloud_notm}} SAML service provider](images/IBM-Cloud-SAML-provider-login-sqeuence.svg "Login process for users who are connected from {{site.data.keyword.cloud_notm}} SAML service provider"){: caption="Login process for users who are connected from {{site.data.keyword.cloud_notm}} SAML service provider" caption-side="bottom"}

1. The user starts the sequence by visiting an account-specific URL with their browser. This is either `https://cloud.ibm.com/authorize/<account id>` or `https://cloud.ibm.com/authorize/<account alias>`. The account alias can be configured on the IAM Identity Provider configuration pages in the IBM Cloud console.
1. The IBM Cloud console redirects the user's browser to IBM Cloud's IAM component. As part of the redirect, the account ID or alias is sent to IAM.
1. The SAML request is sent to the enterprise customer's user authentication and authorization system.
1. After validating the user's credentials, the enterprise customer's system sends a redirect instruction to the user's browser. Part of this redirect is the SAML response containing assertions that describe the user and the additional attributes of that user.
1. The browser completes the redirect and sends the SAML response with assertions to IAM.
1. After validating the SAML response, IAM is now finishing its authentication flow with the console by sending an OAuth2 compliant redirect with an authorization code to the browser.
1. The browser provides the authorization code to the console, which in turn is used to retrieve the required tokens from IAM.
1. When the console receives the tokens, the login sequence ends. The console can now invoke IBM Cloud APIs and identify the user.
1. The dashboard with with user-specific content is displayed.

## Login sequence for IdP-initiated login flow
{: #idp-initiated-login}

IdP-initiated login allows the login sequence to be triggered from the external SAML IdP rather than from the {{site.data.keyword.cloud_notm}} login URL. This flow allows users to start their authentication directly from their enterprise identity provider portal. The IdP-initiated login sequence in {{site.data.keyword.cloud_notm}} works according to the following sequence:

![Login process for IdP-initiated login flow](images/idp-initiated-login.svg "Login process for IdP-initiated login flow"){: caption="Login process for IdP-initiated login flow" caption-side="bottom"}

1. The user enters their credentials to log in to the Federation IdP. The enterprise customer's system validates the user's credentials.

2. After successful validation, the Federation IdP creates a SAML assertion containing information that describes the user and their additional attributes, and redirects the browser.

3. The browser is redirected with the SAML assertion to {{site.data.keyword.cloud_notm}}'s IAM component. IAM validates the SAML assertion and creates an authorization code.

4. The browser sends the authorization code to the {{site.data.keyword.cloud_notm}} console.

5. The console exchanges the authorization code with IAM for tokens.

6. IAM provides the access tokens to the console.

   OAuth2 tokens are exchanged directly between the console and IAM servers, to maintain security throughout the flow.
   {: tip}

7. The authentication flow is complete. The console can now use {{site.data.keyword.cloud_notm}} APIs and identify the user.

8. The user is logged in and the dashboard with user-specific content is displayed.
