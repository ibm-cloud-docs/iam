### Federating users to {{site.data.keyword.cloud_notm}}
{: #federate-users-iam}

{{site.data.keyword.cloud_notm}} offers two federation options that enable your employees to access {{site.data.keyword.cloud_notm}} with their company credentials: [federate with IBMid](https://www.ibm.com/docs/en/ief){: external} or create an {{site.data.keyword.appid_full_notm}} service instance. For more information, see [Enabling authentication from an external identity provider](/docs/iam?topic=iam-ibm-idp-integration).

Both options require users to be account members or have access through a trusted profile. With IBMid federation, account owners or administrators must invite users, who become active members after accepting. With {{site.data.keyword.appid_short}}, users are automatically onboarded without invitations. In both cases, federated users can access IAM-enabled resources and classic infrastructure based on their assigned access.

Trusted profiles handle federated users differently. Users' SAML-based IdP attributes are evaluated at login, and if they meet the trusted profile conditions, users are prompted to apply one or more profiles. Trusted profiles grant time-limited access (typically 1-4 hours) for specialized tasks, enabling frequent authentication checks for reduced security risks. Users are automatically added through the trust relationship without onboarding. When a user leaves your company, deleting their corporate identity in your directory revokes {{site.data.keyword.cloud_notm}} access.
