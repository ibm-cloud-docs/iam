---

copyright:

  years: 2019, 2026
lastupdated: "2026-03-31"

keywords: token, token expiration, settings, access token, refresh token, IAM

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Setting limits for IAM tokens
{: #token-limit}

As an account owner or user assigned the administrator role for the Identity service, you can meet your security requirements by setting custom expiration values for tokens. Identity and Access Management (IAM) access tokens and refresh tokens can both be customized for token limits.
{: shortdesc}

Token expiration settings apply only when there is no connected login session. For more information, see [Determining when sessions are created](#sessions-nonsessions).
{: note}


## Before you begin
{: #before-limits}

If you have the following access, you can update the settings for token expiration:

- Account owner
- Operator or admin role on all account management services
- Operator or admin role on IAM Identity service

For more information about access, see [Actions and roles for account management services](/docs/iam?topic=iam-account-services&interface=ui#account-management-actions-roles).

## Managing access token expiration
{: #accces-token-limit}

IAM access tokens can be used to invoke various {{site.data.keyword.cloud_notm}} APIs. This is a temporary credential that is the result of an authentication. After the acquired access token expires, a refresh token is used to get a new access token so that you can continue calling {{site.data.keyword.cloud_notm}} or service APIs.

To update your access token expiration setting, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Settings**.
1. From the Login session section, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") on the Access token tile.
1. Enter the time limit in minutes. An access token can be valid for up to 60 minutes.
1. Click **Save**.

## Managing refresh token expiration
{: #refresh-token-limit}

When available, this credential is used to get a new access token without reauthentication. This token isn't sent to APIs and is used only to get new access tokens.

To update your refresh token expiration setting, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Settings**.
1. From the Login session section, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") on the Refresh token tile.
1. Enter the time limit in hours. A refresh token can be valid for up to 72 hours (3 days).
1. Click **Save**.


## Determining when sessions are created
{: #sessions-nonsessions}

Sessions are created when a user logs in to the {{site.data.keyword.cloud}} CLI or {{site.data.keyword.cloud}} console. For example, if you create a user API key and use it for the {{site.data.keyword.cloud}} CLI, this generates a login session. However, if you use the same API key to create a token for API calls, like [creating an IAM access token for a user or service ID](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey), this does not generate a session.

Tokens expiration settings apply only if there is no connected login session. If a login session is created, then [limits for login sessions](/docs/iam?topic=iam-iam-work-sessions) apply. Use the following table to help you understand when each setting applies.

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| {{site.data.keyword.cloud}} CLI | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |                                                |                                                |
{: caption="Sessions and refresh token availability - Users" caption-side="bottom"}
{: summary="When a session is created or not depends on a combination of the identity type and login type."}
{: #table01}
{: tab-title="Users"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| {{site.data.keyword.cloud}} CLI | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |                                                |                                                |
{: caption="Sessions and refresh token availability - Trusted profiles for federated users" caption-side="bottom"}
{: summary="When a session is created or not depends on a combination of the identity type and login type."}
{: #table02}
{: tab-title="Trusted profiles - federated users"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}

| Login type | Sessions | Refresh tokens |
|------------|----------|----------------|
| {{site.data.keyword.cloud}} Console | N/A | N/A |
| {{site.data.keyword.cloud}} CLI |         | ![Checkmark icon](../icons/checkmark-icon.svg) |
| API call                        |         |                                                |
{: caption="Sessions and refresh token availability - Service IDs" caption-side="bottom"}
{: summary="When a session is created or not depends on a combination of the identity type and login type."}
{: #table03}
{: tab-title="Service IDs"}
{: tab-group="Identity type"}
{: class="comparison-tab-table"}
{: row-headers}


## Next steps
{: #next-reading-tokens}

For more information about using IAM access tokens, see the following topics:

* [Invoking {{site.data.keyword.cloud_notm}} service APIs](/docs/iam?topic=iam-iamapikeysforservices)
* [Generating an {{site.data.keyword.cloud_notm}} IAM token by using an API key](/docs/iam?topic=iam-iamtoken_from_apikey)
