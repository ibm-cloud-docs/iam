---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-31"

keywords: classic infrastructure API keys, classic infrastructure API, SoftLayer API key

subcollection: iam

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:note: .note}
{:tip: .tip}

# Managing classic infrastructure API keys
{: #classic_keys}

You can use classic infrastructure API keys to access classic infrastructure APIs. You can have only one classic infrastructure API key per user, and each user can create, delete, and view the details for their API key. If you are an ancestor in the classic infrastructure hierarchy for a user, you can also edit or delete those user's API keys.
{: shortdesc}

{{site.data.keyword.cloud}} [API keys](/docs/iam?topic=iam-userapikey#create_user_key-api) can also be used to access classic infrastructure APIs.
{: tip}

To manage classic infrastructure API keys, go to **Manage** > **Access (IAM)** > **API keys**, and select **Classic infrastructure API keys** in the {{site.data.keyword.cloud_notm}} console. You can see your classic infrastructure API key and any API keys for users that you are an ancestor for in the user hierarchy, meaning you invited the user or someone you invited to the account invited the user, and so on.

## Creating a classic infrastructure API key
{: #create-classic-infrastructure-key}

When you create a classic infrastructure API key, you can use the IP address restrictions feature on the **User details** page. To create a classic infrastructure API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**, and select **Classic infrastructure API keys**.
2. Click **Create a classic infrastructure key**.
   If you don't see this option, check to see if you already have a classic infrastructure API key that is created because you're only allowed to have one in the account per user.
   {: note}

3. Copy or download the API key, and save it in a safe place. You can retrieve the details of the API key later.

To get the details of a classic infrastructure API key after you create it, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **View details**. You can copy the API key value.

To get the details of a classic infrastructure API key after you create it, go to **Manage** > **Access (IAM)** > **Users** in the {{site.data.keyword.cloud_notm}} console, then select the user's name. From the API keys section, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **View details** in the row for the classic infrastructure API key row. You can copy the API key value.

In most cases, the username of your classic infrastructure API key will be your `<account_ID>_<email_address>`. It is the same as your VPN username displayed on your User details page in the VPN password section.
{: tip}

To delete a classic infrastructure API key, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete** on the row for the API key in the API keys section.

## Managing other user's classic infrastructure API keys
{: #user-classic-infrastruture-keys}

If you are an ancestor in the classic infrastructure hierarchy for a user, you can view and delete classic infrastructure API keys for users, including VPN only users.

Only users who create the API key can retrieve the API key value after it's created.
{: note}

In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **API keys**, and select **Classic infrastructure API keys**. Then, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and select actions whether it's to view the details or delete the API key.
