---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: restrict domain, restrict invitation, account member restrict, invitation, invite users, account restriction

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Restricting domains for account invitations
{: #restrict-acct-invite}

You can restrict membership to your account based on the domain of the users that are added to your allowlist. This way, only users with a specific domain or domains can be invited to the account. To update this setting, you must be assigned the `editor` role or higher on the IAM Identity Service.

Domain restrictions are implemented by setting email patterns. For example, `**@ibm.com`, `**@*.ibm.com`, `**@?.ibm.com`. A single asterisk `*` represents any sequence of zero or more characters in a string, except the sequence ends if a period `.` or at sign `@` is found. A double asterisk `**` represents any sequence of zero or more characters in the string without limit. A question mark `?` represents any single character.

Let's take a closer look at the example `**@*.ibm.com`. The username part of the email address specifies `**`. Since the sequence is not limited by `.`, an email address like `my.name.is.bob@us.ibm.com` is valid. The subdomain `us` is also valid because it is a string of letters, where the sequence ends with `.`.

## Enabling domain restrictions for account invitations
{: #restrict-domain-enable}

To enable domain restrictions for account invitations, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)** > **Settings**.
1. In the Account section, enable **Restrict user domains**.
1. Enter the domains that can access the account. Any domain that isn't added to this list is restricted.
1. Click **Add**.
1. Click **Save**.

## Disabling domain restrictions for account invitations
{: #restrict-domain-disable}

When you disable the User domains setting, you can send account invitations to any domain, which removes the previously set allowed domain access. To disable restrictions on specific domains, complete the following steps:

1. Go to **Manage** > **Access (IAM)** > **Settings** in the {{site.data.keyword.cloud_notm}} console.
1. In the Account section, disable the **Restrict user domains** setting.
1. Select an option for disabling the setting.
   1. To disable the setting and save the allowlist of domains, select **Disable and save domains**.
   1. To disable the setting and delete the allowlist, select **Disable and delete domains**.
1. Click **Yes**.
