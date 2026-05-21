---

copyright:

  years: 2021, 2026
lastupdated: "2026-05-21"

keywords: frequently asked questions, cbr faqs, cbr and iam, context-based restrictions, access restrictions

subcollection: iam

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about Context-based restrictions
{: #cbrfaq}

FAQ for {{site.data.keyword.cloud}} Context-based restrictions might include questions about access restrictions for {{site.data.keyword.cloud_notm}} resources.
{: shortdesc}

To find all FAQ for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).

## What are {{site.data.keyword.cloud_notm}} Context-based restrictions?
{: #whatiscbr}
{: faq}
{: support}

As an account owner or administrator, you can define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the network location of access requests by enabling Context-based restrictions. For more information, see [What are context-based restrictions?](/docs/iam?topic=iam-context-restrictions-whatis).

## How do you use Context-based restrictions and IAM policies together?
{: #iam-cbr-diff}
{: faq}

These restrictions work with traditional IAM policies, which are based on identity, to provide another layer of protection. Since both IAM access and Context-based restrictions enforce access, Context-based restrictions offer protection even in the face of compromised or mismanaged credentials.

Unlike IAM policies, Context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed Context that you configure.
{: note}

## What's the difference between Context-based restrictions and allowed IP addresses?
{: #ip-cbr-diff}
{: faq}

 Context-based restrictions enforce access restrictions at the individual service level and access is evaluated when a user attempts to access a resource. Allowed IP address restricts access at the account level, which is evaluated at login.

## How can I make sure that my rule doesn't break an access flow?
{: #monitor-cbr-faq}
{: faq}

As an administrator, you manage users, applications, and workflows that depend on having the correct access when they need it. To make sure that your Context-based restrictions rules don't brake an access flow, set the rule to report-only mode for at least 30 days before you enable the rule. This way, you can monitor the impact of the rule on your access flows, such as when access is denied or allowed and for which identities. For more information, see [Monitoring context-based restrictions](/docs/iam?topic=iam-cbr-monitor).

## How can I create GEO-based restrictions for account access by using Context-based restrictions in {{site.data.keyword.cloud_notm}}?
{: #geobased-restrictions}
{: faq}

Currently, {{site.data.keyword.cloud_notm}} does not support GEO-based account access control through Context-based restrictions. This is a known limitation within the platform, and such a functionality is not available now.

## Can I manage context-based restrictions with Terraform?
{: #faq-terraform-cbr}
{: faq}

Yes. Implement zero-trust security with the [Context-Based Restrictions module](https://registry.terraform.io/modules/terraform-ibm-modules/cbr/ibm/latest){: external} for automated zone and rule management. Review [Terraform IBM Modules](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about-tim) for security patterns.
