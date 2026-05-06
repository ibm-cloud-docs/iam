---

copyright:

  years: 2022, 2026
lastupdated: "2026-05-06"

keywords: users level of access, user control, access control, permissions, manage access, access management, platform management tasks, assign roles, fine-grained access, least privilege

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# IAM access concepts
{: #access-management-overview}

{{site.data.keyword.cloud_notm}} IAM follows an [eventually consistent](https://en.wikipedia.org/wiki/Eventual_consistency){: external} pattern that is common to many cloud-native services. As a result, IAM remains highly available and performant across multiple global regions. Changes that are made to IAM access policies, authorizations, service IDs, API keys, access groups, trusted profiles, resource groups, users, or any other access controls are recorded and propagated across all IAM components and IAM-enabled services worldwide. Access changes might not take effect until the propagation process is complete.
{: shortdesc}

## Access groups
{: #access-groups-iam}

A group of users and service IDs can be organized so that the same access can be assigned to all members within the group by using one or more policies. With access groups, you can streamline the access assignment process so that you can manage fewer policies and reduce the number of policies in an account, which in turn increases performance. Access groups allow you to grant and revoke access by simply adding or removing users or service IDs in the access group. After your groups are set up, you can start assigning policies by selecting an access group as the subject of the policy. For more information, see [Setting up access groups](/docs/iam?topic=iam-groups).

## Trusted profiles
{: #trusted-profiles-iam}

With trusted profiles, you manage the identities of your users within your own corporate directory. And, you can centrally manage the access lifecycle to multiple {{site.data.keyword.cloud_notm}} accounts and assets for federated users without the need to configure access policies for each entity within each account. You don't need to invite users to your account to give them to access your {{site.data.keyword.cloud_notm}} resources.

You can also define fine-grained authorization for all applications that are running in a compute resource without creating service IDs or managing the API key lifecycle for applications. To start creating trusted profiles for your organization, see [Creating trusted profiles](/docs/iam?topic=iam-create-trusted-profile).

## Resources
{: #resources-access-management}

Account resources are the service instances that are selected from the catalog or finer-grained resources within a service instance, such as an {{site.data.keyword.cos_full}} bucket. IAM-enabled resources are added to a resource group when they are created from the catalog.

IAM access management enables fine-grained access, which means that a policy can be set on a wide scale to all resources in a resource group, for example, or to a specific service instance in the account and even a resource type like an {{site.data.keyword.cos_full_notm}} bucket within a specific instance.

## Access policies
{: #access-policies-concept}

Access policies are how users, [service IDs](/docs/iam?topic=iam-serviceids), access groups, and trusted profiles in the account are given permission to access and take actions on account resources. Policies include a subject, target, and role. The subject is the user, service ID, or access group that you are providing access. The target of the policy is the resource to which you want to provide access. And, the IAM roles define the level of access or allowed actions on the target of the policy.

A policy assigns the subject one or more roles that define the level of access and one or more attributes that define the target that the policy allows access to. The policy can provide access to a single service at the instance level, to a set of resources that are organized together in a resource group or to any set of resources that can be defined by a set of attributes such as location or resource type. A policy can also provide access to account management services. Depending on the IAM roles that you assign, the subject is allowed varying levels of access for completing account management tasks, working with service instances, or accessing a service by using the console or completing API calls.

There are different types of policies that allow access to account resources for users and service IDs: a resource group policy, a resource instance policy, an account-wide policy for access to all IAM-enabled services or all instances of a specified service, and a policy on all or one account management services. Depending on your selections, custom configuration options, such as defining access to resources in a specific location or defining access to the granular level of a service-specific resource within an instance, might be available.

In addition to access policies for users and service IDs, there is a policy type that is called an authorization that allows specific services or instances of services access to other services. You can learn more about assigning access between services in the [Using authorizations to grant access between services](/docs/iam?topic=iam-serviceauth) documentation.

## Roles
{: #iam-roles-concept}

{{site.data.keyword.cloud_notm}} access roles are a group of actions. Access roles allow users and service IDs to complete specific tasks within the context of the target resources that are defined in the policy. There are two types of predefined access roles: platform management and service access. The third type of access role is a custom role that you can create for a service to combine any set of available actions to meet your organizational needs.

Platform management roles define allowable actions, such as assigning user access and creation of service instances, for managing resources at the platform level. Platform roles also apply to actions that can be taken within the context of account management services, such as inviting and removing users, managing access groups, managing service IDs, and private catalog products.

Service access roles define allowable actions, such as calling service APIs or accessing a service's dashboard. These roles are customized based on the service that is selected within the policy.

When you assign access within the console, next to the role you can see the number of actions that are mapped to each role and drill down into that list to see exactly what each role allows.
{: tip}

For more information, see [IAM roles](/docs/iam?topic=iam-userroles#iamusermanrol).

## Actions
{: #iam-roles-actions}

Actions are mapped to {{site.data.keyword.cloud_notm}} IAM roles so that users can perform only specific tasks when they are assigned the different roles. Sometimes actions are also referred to as permissions or operations. Allowable actions for each role change based on the service that is being accessed because each service defines how that role maps to the use of the service. For more information, see [IAM roles and actions](/docs/iam?topic=iam-iam-service-roles-actions).

## Enterprise-managed IAM templates
{: #enterprise-iam-concept}

Enterprise-managed IAM templates are a useful tool for standardizing access management and account security settings across an [enterprise](x2026915){: term}. Templates allow you to define commonly used access groups, trusted profiles, and security settings in a consistent manner, ensuring that your security policies are applied uniformly throughout the enterprise. This can be especially important for compliance with organizational standards, which may require that certain access management and security settings are configured consistently across all or some accounts. By using IAM templates, you can simplify the management of your security policies, reduce the risk of misconfiguration or human error, and improve overall security posture. For more information, see [How enterprise-managed IAM works](/docs/enterprise-management?topic=enterprise-management-access-enterprises#how-enterprise-iam).

Enterprise-managed IAM resources in your child account have the tag [enterprise-managed]{: tag-cyan}.
{: note}

### Action controls
{: #action-controls-concept}

Action controls enforce your preferences on which operations child account administrators can take on the enteprise-managed IAM resources in their accounts. You might want to allow child account administrators to add members to an enterprise-managed access group that you assign in their account. In this case, you can enable the action control for adding members. Or, you might want to prohibit child account administrators from adding new policies to a trusted profile. By default, action controls restrict child account administrators from making changes to enterprise managed IAM resources in their account.

## Access management system
{: #access-management-system}

The {{site.data.keyword.cloud_notm}} IAM control system allows or denies actions by users or service IDs within the context of a service based on their assigned access policies. By default, every user and service ID has no access. Each access policy that is added enables the user or service ID to perform an action within the account based on the specified target and role that is selected in the access policy. When a user tries to complete a specific action, the control system uses the attributes that are defined in the policy to determine whether the user has permission to perform that task. For more information, see [How {{site.data.keyword.cloud_notm}} IAM works](/docs/iam?topic=iam-iamoverview).

### What is ABAC and RBAC?
{: #whatis-abac-rbac}

There are two common types of IAM systems in cloud providers and understanding each of these models can help you gain a better understanding of how IAM works in {{site.data.keyword.cloud_notm}}.

* Attribute-based access control (ABAC) uses attributes from identities, such as users and service IDs, environments, and resources. These attributes are used by an access decision engine to determine whether an access request should be permitted or denied. ABAC provides more flexibility, control, and features than role-based access control systems. ABAC is typically used when fine-grained access control is needed, or if a wide variety of access control use cases needs to be solved by the same decision engine. ABAC helps reduce security risks by providing fine-grained access control and is typically more complex, especially during initial setup.

* Role-based access control (RBAC) uses a mapping from an identity, such as a user or service ID, to a role. The RBAC role defines the type of access that an identity with the RBAC role can take against a resource. Typically access can be granted for a resource type or a grouping of resources. RBAC roles are usually defined based on job responsibilities within an organization. The RBAC role grants the access that is needed for an identity to do its job. This is a simple model because IAM administrators manage the mapping of RBAC roles to an identity. RBAC roles setup can be simpler than ABAC initial setup.

{{site.data.keyword.cloud_notm}} IAM uses an ABAC model by using identity and resource attributes. {{site.data.keyword.cloud_notm}} IAM uses access policies to store the attribute information that is needed by the IAM access decision engine. And, the access policies tell the IAM decision engine, which attributes the author of the policy requires to grant access to a resource.

The supported attributes for identities are iam_id and access group ID. The supported attributes for resources belong to one of the following categories:
* Fields defined in the resource [CRN](/docs/account?topic=account-crn), for example the service name.
* System-wide defined resource attributes, such as resource groups.
* Service-specific resource attributes such as namespaces or buckets.

Each service defines the supported attributes for resources it manages. For more information, see the documentation for the service you're using.
{: note}

A best practice in {{site.data.keyword.cloud_notm}} IAM is to use access groups to manage access for identities. After the access group access policies are defined, granting, and revoking access is simply a matter of adding and removing identities to or from access groups. A user or service ID can belong to as many access groups as the administrator wants, and the members of the group inherit all access that is assigned to the access group. This approach provides the fine-grained access benefits of ABAC with the simplicity of RBAC.

IAM administrators familiar with RBAC might use access groups to mimic an RBAC model. Conceptually an access group is similar to an RBAC role. If you're more familiar with using traditional RBAC roles like system administrator, network administrator, or storage administrator, these can be defined in {{site.data.keyword.cloud_notm}} IAM by using access groups with specific access policies that are assigned to each.
{: tip}

For example, you can create an access group called `Storage Administrators`. When it is first created, no access is granted to any members of the access group. The access group can then be assigned policies granting the Administrator role to all storage resources in the current account as well as any that will be created in the future. If a new user joins the team and their job in the organization is a storage administrator for the account, then they can simply be added to the access group and have all of the access that they need to do their job.

This is a simple example, but the approach can be applied to any job, role, or responsibility in an organization. The access policies assigned to the access group can be fine-grained allowing for use cases like storage administrator of all storage in a specific resource group, and even for only a specific storage type.

For more information about getting up and running quickly with {{site.data.keyword.cloud_notm}} IAM by setting up access groups for quick access assignments, inviting users to your account, and managing their access, see [Assigning access to resources](/docs/iam?topic=iam-access-getstarted).
