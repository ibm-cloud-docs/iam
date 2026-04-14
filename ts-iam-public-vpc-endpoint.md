---

copyright:

  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot context-based restrictions, VPC, public endpoint

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my rule for all endpoint types from VPC not working as expected?
{: #troubleshoot-cbr-vpc-public-endpoint}
{: troubleshoot}

If you create a context-based restrictions rule for VPC that allows all endpoint types, the network zone for your rule must be configured correctly.
{: shortdesc}

When you create a context-based restrictions rule for VPC that allows all endpoint types, access from the VPC to the public endpoint is denied while the private endpoint returns the expected results. You might need to reconfigure your network zone.
{: tsSymptoms}
   
The public gateway's associated IP addresses are not included in the zone definition along with the VPC.
{: tsCauses}

To include the public gateway's associated IP addresses in the zone definition, complete the following steps. To update a network zone, you must be the account owner or be assigned the administrator or editor role on the Context-based restrictions account management service.
{: tsResolve}

1. Go to **Manage** > **Context-based restrictions** in the {{site.data.keyword.cloud_notm}} console, and click **Network zones**.
2. Select the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") for the network zone that you want to update, and select **Edit**.
3. Update the list of allowed IP addresses to include the public gateway's associated IP addresses. For more information, see [Retrieve a public gateway](/apidocs/vpc/latest?code=node#get-public-gateway).
4. Click **Next** to review your new configuration.
5. Click **Update** to apply the changes.
