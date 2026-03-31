---

copyright:

  years: 2017, 2026
lastupdated: "2026-03-31"

keywords: access management, user management, access groups, fine-grained access, centralized management, least-privilege access, workload security, enterprise access control, defense in depth

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Access management features
{: #access-mgmt-features}

{{site.data.keyword.cloud}} Identity and Access Management (IAM) provides powerful features for managing user access and implementing least-privilege access principles across your enterprise workloads.
{: shortdesc}

## User management
{: #usermgmt-feature}

With unified user management, you can add and delete users in an account for both platform and classic infrastructure services. You can organize a group of users in an access group to make assigning access for more than one user or service ID at a time a quick and easy task.

## Fine-grained access control
{: #fgaccess-feature}

Access for users, service IDs, access groups, and trusted profiles are defined by a policy. Within the policy, the scope of fine-grained access can be assigned to a set of resources in a resource group, a single resource, or account management services. After the target is set, you can define what actions are allowed by the subject of the policy by selecting access roles. Roles provide a way to tailor the level of access that is granted for the subject of the policy to perform actions on the target of policy, whether it is platform management tasks within the account or accessing a service's UI or completing API calls. This approach supports least-privilege access principles and defense in depth security strategies.

You can also add time-based conditions to a policy that defines when the policy grants access, whether you want to grant temporary access to resources in your account or allow access during recurring time windows. For more information, see [Limiting access with time-based conditions](/docs/iam?topic=iam-iam-time-based).

## Access groups for streamlined access management
{: #access-groups-quick-access}

Quickly and easily assign access for a group of users, service IDs, or trusted profiles that are organized in an access group by assigning access to the group, and then add or remove identities as needed to grant or deny access to account resources. Access groups enable centralized management of a minimal number of policies in the account, supporting enterprise-scale workload security. For more information, see [Setting up access groups](/docs/iam?topic=iam-groups).

## Next steps
{: #access-mgmt-next-steps}

* Learn about [trusted profiles](/docs/iam?topic=iam-trusted-profiles-overview) for federated users and compute resources.
* Explore [authentication features](/docs/iam?topic=iam-authentication-features) including API keys and MFA.
* Review [IAM concepts](/docs/iam?topic=iam-access-concepts) for a deeper understanding of access management.
