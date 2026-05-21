---

copyright:

  years: 2017, 2026
lastupdated: "2026-05-06"

keywords: users level of access, user control, access control, permissions, manage access, access management, platform management tasks, assign roles, centralized, enterprise scale

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Centralized access management across your organization
{: #cloudaccess}

Control user access to IBM Cloud resources with centralized access management. Assign roles and policies to manage permissions at enterprise scale.
{: shortdesc}

Access management enables you to control which users see, create, use, and manage resources in your account. To grant access following least privilege principles, you can assign roles that allow users fine-grained levels of access for completing platform management tasks and accessing account resources.

The way that you manage access in {{site.data.keyword.Bluemix}} depends on the type of resource that you want to assign access to. {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) is the access management system that is used for consistently managing resources that are organized in a resource group across the {{site.data.keyword.cloud_notm}} platform. [Classic infrastructure resources](/docs/iam?topic=iam-mngclassicinfra) are not managed by using IAM. These resource types have their own access management systems.

If you have a combination of resource types, you manage each type separately:

* For [IAM resources](/docs/iam?topic=iam-userroles), go to **Manage** &gt; **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and then select **Users**, **Access groups**, **Trusted profiles**, or **Service IDs** to get started.
* For assigning access to your classic infrastructure resources, you set permissions within **Manage** > **Access (IAM)** on the Classic infrastructure tab for the user that you want to assign access. You can also choose to assign Classic infrastructure access by using **Trusted profiles** if your account is linked to a Softlayer account.

While each type of access is managed separately, all access policies are made up of a subject you want to assign access to, a target for the policy to scope what the subject has access to, and then finally an IAM role or classic infrastructure permission to determine the level of access the subject has on the target.

![Access management policies by using IAM or classic infrastructure permissions.](images/access-management.svg "How assigning policies works by starting with a subject, selecting a target, then assigning a role or permission"){: caption="Access management policies by using IAM or classic infrastructure permissions" caption-side="bottom"}

For IAM policies, the subject can be an access group, user, service ID, or trusted profile. And, the target can be an account management service, resource group, service in the account, specific service instance, or resource type within a service. Platform and service roles can be selected to scope the level of access for the subject. For classic infrastructure, a user is selected, and then the access can be scoped to a service or device with specific permissions assigned. For classic infrastructure that doesn't support the use of IAM policies for managing access, see [classic infrastructure permissions](/docs/iam?topic=iam-mngclassicinfra#how-classic-infra-permissions-work).

## {{site.data.keyword.cloud_notm}} IAM limits
{: #iam_limits}

The following table lists the maximum limits for IAM resources. These limits apply to any user who can create IAM resources. If a limit is exceeded, you receive an exception and are not allowed to create any new resources beyond that limit.

If you have a specific use case that requires an extended limit, you can request an increase. For more information, see [Increasing account limits](/docs/iam?topic=iam-account-limits).
{: note}

| Resource                               | Max  |
|----------------------------------------|------|
| Access groups per account              | 500  |
| Access groups per user                 | 50   |
| Access management tags per account     | 250  |
| API Keys per identity                  | 20   |
| Custom roles per account               | 40   |
| Dynamic rules per access group         | 5    |
| Dynamic rules per trusted profile      | 20   |
| Dynamic rules per Identity provider (IdP) | 2000 |
| IdPs per account  | 5    |
| Policies per account [^tabletext]      | 4020 |
| Policies per subject within an account | 1000 |
| Policies with access management tags within an account   | 500   |
| Service IDs per account                | 2000 |
| Trusted profiles per account           | 2000 |
| Users per trial account                | 100  |
| Users per billable account             | 7500 |
{: caption="IAM account limits" caption-side="top"}

[^tabletext]: IAM policies and context-based restrictions rules share a combined limit of 4020.

A maximum of 1,000 policies and service to service authorizations within one account is recommended to ensure optimal performance within your account. For more information about limiting the number of policies in your account, see the [Best practices for organizing resources and assigning access](/docs/account?topic=account-account_setup).
{: tip}

If you want to check the number of policies in your account, see [Viewing the total number of policies per account](/docs/iam?topic=iam-account-limits&interface=cli#total-number-policies-cli). To request an increase in the account limit, see [Requesting a policy and rule shared limit increase](/docs/iam?topic=iam-account-limits&interface=cli#limit-increase).
