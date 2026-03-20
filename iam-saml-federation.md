---

copyright:

  years: 2019, 2026
lastupdated: "2026-03-20"

keywords: enterprise SSO

subcollection: iam

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:deprecated: .deprecated}
    
# Managing deprecated SAML federation
{: #saml-federation}

If you previously set up federation by using a SAML identity provider (IdP) in the SoftLayer customer portal, you can edit the IdP configuration data or delete it from the Identity providers page in the {{site.data.keyword.Bluemix}} console. 
{: shortdesc}

This type of federation is deprecated. If you delete this configuration, it is permanent and you can't set it up again. You can now take advantage of federation with IBMid. For more information, see [Setting up your IBM Cloud account](/docs/account?topic=account-account-getting-started).
{: deprecated}

To edit your SAML configuration data, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and then select **Identity providers**. 
2. Click **Edit**.
3. Change the information in the fields that you need to edit.
4. Click **Save**.

To delete your deprecated SAML federation configuration, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and then select **Identity providers**. 
2. Click **Delete**.
3. Select the option to confirm that you understand deleting the configuration is permanent. Since this type of federation is deprecated, it can't be set up again.
4. Click **Delete**.
