---

copyright:

  years: 2020, 2026
lastupdated: "2026-04-06"

keywords: troubleshoot access to a resource, why can't user access resource

subcollection: iam

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't a user in my account access resources from the Resource list page?
{: #troubleshoot-serviceaccess}
{: troubleshoot}

Users in your account must have access to the service or service instance and the containing resource group to access the instance from the Resource list page.
{: shortdesc}

A user has an access policy on a specific resource or a service in the account, but they can't access the service from the Resource list page.

When the user selects the service name, the following error message is displayed:
{: tsSymptoms}

```text
You do not have access to any organizations, spaces, or resource groups in this region. Check that you have the appropriate access with your account owner or administrator.
```

In addition to access to the type of service or specific resource, the user must also be assigned access to the resource group or space that contains the resource. To access the resource instance within a specific account, a user must be assigned at least the Viewer role or higher on the resource group itself.
{: tsCauses}

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)**, and select the user's name from **Users** page.
1. From the row for the user that you want to assign access, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and click **Assign access**.
1. Select the service. Then, click, **Next**.
1. Scope the access to a specific resource group to which you want to allow access. Then, click, **Next**.
1. Select the resource group access. The Viewer role is sufficient to enable the user to access the resource. Then, click, **Next**.
1. Select the roles that you want the user to have.
1. Click **Review**.
1. Click **Add** to add the access to the access summary.
1. Click **Assign**.
{: tsResolve}
