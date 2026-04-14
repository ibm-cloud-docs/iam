---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-31"

keywords: network-level access, network security strategy
subcollection: iam
content-type: tutorial
account-plan: lite
completion-time: 20m

---

{{site.data.keyword.attribute-definition-list}}

# Leveraging context-based restrictions to secure your resources
{: #context-restrictions-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="20m"}

This tutorial walks you through how to use context-based restrictions as another layer of protection to your resources. By completing this tutorial, you learn how to create network zones and rules that define access restrictions to specific resources based on context in addition to IAM identity. For more information, see [What are context-based restrictions?](/docs/iam?topic=iam-context-restrictions-whatis)
{: shortdesc}

The tutorial uses a fictitious account owner named Xander. Xander previously set up access for managers that need the `administrator` role on account management services by using IAM policies.

Xander trusts his team to manage their personal and service credentials properly, but he wants to make sure they are protected even if credentials are mismanaged. Because Xander knows the IP addresses that the team uses, Xander can restrict access to the access management service based on the network location of the access requests. This way, access policy creation is restricted to the IP addresses he defines. Since both IAM access and context-based restrictions must allow access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials.

## Before you begin
{: #cbr-tutorial-before-you-begin}

Set up {{site.data.keyword.cloudaccesstrailshort}} to monitor your enabled and report-only rules. For more information, see [Monitoring context-based restrictions](/docs/iam?topic=iam-cbr-monitor).

## Create a network zone
{: #tutorial-networkzone-new}
{: step}

First, create a new network zone for the team.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**
2. Go to **Network zones** and then click **Create**.
3. Name the network zone `management-team-zone`
4. Enter the IP addresses the team must use:
    1. Team members in Austin use the following IP addresses: 4.4.4.1-4.4.4.99
    1. An Austin team member in another building uses the following subnet: 204.17.5.0/24
    1. A remote team member uses the following IP address: 3.3.3.56
5. Click **Next**.
6. Review the details of the network zone.
7. Click **Create**.

## Create a rule
{: #tutorial-context-rules}
{: step}

Now, Xander can use the network zone that he created in a rule.

1. Go to **Rules** and click **Create**.
1. To restrict access to the creation of IAM policies, select the **IAM Access Management Service**.
1. Click **Continue**.
1. Xander has public endpoints in his network zone, so he keeps the endpoint type toggle switch set to **No**, which allows requests from any endpoint type.
1. Select the network zone `management-team-zone`.
1. Click **Add** to include your context configuration in the rule.
1. Click **Continue**.
1. Name the rule `Management team`
1. Set the enforcement to **Report only** so that you can monitor the impact of the rule before you enable it.
   You can update the enforcement at any time after you create the rule. For more information, see [Updating context-based restrictions](/docs/iam?topic=iam-context-restrictions-update).
   {: note}

1. Click **Continue**.
1. Then, click **Create**.

Xander is logging and monitoring policy management requests by using report-only mode. Since the management team has the correct access policies and use allowed IP addresses, they are authorized to execute policy management operations. All policy management requests that come from IP addresses that don't match the conext that Xander defined are denied when the rule is enabled.

## Next steps
{: #tutorial-context-step-next}

After 30 days of monitoring, update the rule to **Enabled** to begin enforcing your restrictions.

You can also use network zones to restrict access at the account level and user level. For more information, see [Allowing specific IP addresses](/docs/iam?topic=iam-ips).

To create context-based restrictions programmatically, see the [Context-based Restrictions API](/apidocs/context-based-restrictions) and the [Context-based restrictions CLI plug-in](/docs/iam?topic=iam-cbr-plugin).

For more information about implementing context-based restrictions in your security strategy, see the solution tutorial [Enhance cloud security by applying context-based restrictions](/docs/solution-tutorials?topic=solution-tutorials-cbr-enhanced-security).
