---

copyright:
  years: 2020, 2026
lastupdated: "2026-03-20"

keywords: troubleshoot classic infrastructure permissions, what classic infrastructure permission does a user have

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I view classic infrastructure permissions for other users? 
{: #troubleshoot-classicinfra}
{: troubleshoot}

You need specific access to view the classic infrastructure permissions for another user.
{: shortdesc}

Account owners have full access to the {{site.data.keyword.Bluemix}} account, so they do not see the permissions for themselves. Individual users can't edit their own permissions, so they see permissions on their classic infrastructure page, but can't edit them. You must have specific access to view and edit permissions for another user in the account.

You see a message that states that you can't view another user's classic infrastructure permissions.
{: tsSymptoms}
   
You might not be assigned the correct access.
{: tsCauses}

You must ask the account owner to be assigned the permission to manage users, but you must also be an ancestor of the user within the classic infrastructure user hierarchy to view and manage another user's permissions.
{: tsResolve}
