---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: VPN password, update VPN password, classic infrastructure VPN

subcollection: iam

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Updating the classic infrastructure VPN password
{: #vpnpassword}

You can update your own VPN password, or in the case where a user forgets their password and can't reset it themselves, another user with correct access can update that user's VPN password.
{: shortdesc}

If you have the following access, you can update the VPN password for another user:

* An IAM policy with the Editor or higher role on the User management service.
* You are an ancestor in the classic infrastructure hierarchy for the user and you have the Manage users classic infrastructure permission assigned

To update the VPN password, complete the following steps:

1. In the {{site.data.keyword.cloud}} console, click **Manage** > **Access (IAM)**, and select **Users**.
2. Select a user from the list.
3. From the User details page, go to the **VPN password** section.
4. Click the **Edit** icon ![Edit icon](../icons/icon_write.svg "Edit") to enter a new VPN password.
5. Click **Update password**. 
