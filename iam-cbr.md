---

copyright:

  years: 2023, 2026
lastupdated: "2026-03-31"

keywords: iam, context-based restrictions, protecting iam resources, security

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Protecting IAM services with context-based restrictions
{: #iam-services-cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to IAM resources can be controlled with context-based restrictions and identity and access management (IAM) policies. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/iam?topic=iam-context-restrictions-whatis).
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide another layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure.

A user must have the Administrator role on the specific IAM service that you want to target to create, update, or delete rules. A user must also have at least the Viewer role on the Context-based restrictions service to view and add network zones to a rule. The Editor or Administrator roles on the Context-based restrictions service grants users access to create, update, or delete network zones.
{: note}

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated come from the context-based restrictions service, not the IAM service. For more information, see [Monitoring context-based restrictions](/docs/iam?topic=iam-cbr-monitor).

To begin protecting your IAM resources with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/iam?topic=iam-context-restrictions-tutorial).

## How IAM integrates with context-based restrictions
{: #iam-cbr-overview}
{: ui}

To protect a specific IAM service or the group of all IAM Account Management services, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Context-based restrictions**, and select **Rules**.
1. Click **Create**.
1. Select an individual IAM service, or the grouping of all IAM Account Management services.
   - [IAM Access Groups service](/docs/iam?topic=iam-iam-services-cbr&interface=ui#cbr-iam-access-groups)
   - [IAM Access Management service](/docs/iam?topic=iam-iam-services-cbr&interface=ui#cbr-iam-access-management)
   - [IAM Identity service](/docs/iam?topic=iam-iam-services-cbr&interface=ui#cbr-iam-identity)
   - [User Management service](/docs/iam?topic=iam-iam-services-cbr&interface=ui#cbr-user-management)
   - [All IAM Account Management services](/docs/iam?topic=iam-iam-services-cbr&interface=ui#cbr-iam-all)
1. Then, click **Next**.
1. To protect the entire service or group of services, scope the restriction to **All resources**.
1. To protect only a specific set of actions, scope the restriction to **Specific resources**.
   1. Select an attribute and select or enter a value. To learn more about restricting a specific set of actions, review the section for the service that you target in step 3.
1. Click **Review** > **Continue**.
1. Add one or more contexts. Select endpoint types and network zones, and click **Add**. For more information, see [Creating rules](/docs/iam?topic=iam-context-restrictions-create&interface=ui#context-restrictions-create-rules).
1. Click **Continue**.
1. Provide a unique description.
1. Select how you want to enforce the rule. You can decide how you want to enforce a rule upon creation and update the rule enforcement at any time. For more information, see [Rule enforcement](/docs/iam?topic=iam-context-restrictions-whatis&interface=ui#rule-enforcement).

Let's say that you create a rule that targets the IAM Access Groups service. To complete any IAM Access Groups service action, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restricitons rule. For example, a user with the Viewer role on the IAM Access Groups service can complete the action `iam-groups.members.read` if they send the request from the correct network zone and satisfy the rule. If the same user with the Viewer role tries to add a member to the group (`iam-groups.members.add`), they can't complete that request even though they satisfy the rule because they aren't an Editor or Administrator.

To view the actions associated with a service, go to the [Roles](/iam/roles) page in the {{site.data.keyword.cloud}} console.
{: tip}

## How IAM integrates with context-based restrictions
{: #cbr-overview-api}
{: api}

To protect a specific IAM service or the group of all IAM Account Management services, use the following attributes to build your rule:

| Service        | Name           | Value          |
| -------------- | -------------- | -------------- |
| [IAM Access Groups service](/docs/iam?topic=iam-iam-services-cbr&interface=api#cbr-iam-access-groups) | `serviceName` | `iam-groups` |
| [IAM Access Management service](/docs/iam?topic=iam-iam-services-cbr&interface=api#cbr-iam-access-management) | `serviceName` | `iam-access-management` |
| [IAM Identity service](/docs/iam?topic=iam-iam-services-cbr&interface=api#cbr-iam-identity) | `serviceName` | `iam-identity` |
| [User Management service](/docs/iam?topic=iam-iam-services-cbr&interface=api#cbr-user-management) | `serviceName` | `user-management` |
| [All IAM Account Management services](/docs/iam?topic=iam-iam-services-cbr&interface=api#cbr-iam-all) | `service_group_id` | `IAM`
{: caption="Attribute name value pairs that identify a service" caption-side="bottom"}

To protect all actions associated with the service, create a rule without scoping it to specific resources or APIs. For more information, see [Creating rules](/docs/iam?topic=iam-context-restrictions-create&interface=ui#context-restrictions-create-rules). To protect only a specific set of actions, review the following sections, which are linked in Table 1.

## Protecting the IAM Access Groups service
{: #cbr-iam-access-groups}

The IAM Access Groups service includes the ability to create, edit, and delete access groups. The capabilities extend to adding or removing users from groups, assigning access to the group, and managing access for others to work with access groups. You can protect the whole service, which includes all actions associated with the service.

### Restricting the ability to manage a specific access group
{: #cbr-ag-ui}
{: ui}

You can protect the ability to manage a specific access group by scoping a rule to the the `Resource ID` attribute. Creating a rule that is scoped to the `Resource ID` attribute protects all actions associated with the service for that specific access group.

To configure this rule, target the **IAM Access Groups service**, scope the rule to **Specific resources**, and select the `Resource ID` attribute. Then, enter the ID of the access group that you want to protect. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

To find the access group ID, go to **Manage > Access (IAM) > Access groups**. Click the access group that you want to protect in your rule. Then, click **Details**. The value that you want begins with `AccessGroupId`.
{: tip}

### Restricting the ability to manage a specific access group by using the API
{: #cbr-ag-api}
{: api}

You can protect the ability to manage a specific access group by scoping a rule to the the `resource` attribute. Creating a rule that is scoped to the `resource` attribute protects all actions associated with the service for that specific access group.

The following example shows a rule in JSON format that protects a specific access group:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-groups"
				},
				{
					"name": "resource",
					"value": "AccessGroupId1234",
					"operator": "stringEquals"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

To find the access group ID, use the [List access groups](/apidocs/iam-access-groups#list-access-groups) method.
{: tip}

## Protecting the IAM Access Management service
{: #cbr-iam-access-management}

The IAM Access Management service includes the ability to manage custom roles, assign access policies, manage IAM settings, and more. You can protect the whole service, or restrict a specific set of actions based on the context of the request.

### Restricting the ability to manage custom roles in the console
{: #cbr-custom-roles-ui}
{: ui}

You can protect the ability to manage custom roles by scoping a rule to the `Role Management` resource type. Creating a rule that is scoped to the `Role Management` resource type protects the following actions:

- `iam-access-management.customRole.create`
- `iam-access-management.customRole.update`
- `iam-access-management.customRole.delete`
- `iam-access-management.customRole.read`

To configure this rule, target the **IAM Access Management service**, scope the restriction to **Specific resources** > **Resource type**, and then select **Role management**. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

To complete any Role Management action, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restricitons rule. For example, a user with the Viewer role on the IAM Access Management service can complete the action `iam-access-management.customRole.read` if they send the request from the correct network zone and satisfy the rule. If the same user tries to create a custom role, they can't complete that request even though they satisfy the rule because they aren't an Administrator.
{: note}


### Restricting the ability to manage policies in the console
{: #cbr-policies-ui}
{: ui}

You can protect the ability to manage IAM policies by scoping a rule to the `Policy Management` resource type. Creating a rule that is scoped to the `Policy Management` resource type protects the following actions:

- `iam.delegationPolicy.create`
- `iam.delegationPolicy.update`
- `iam.policy.read`
- `iam.policy.create`
- `iam.policy.update`
- `iam.policy.delete`

To configure this rule, target the **IAM Access Management service**, scope the restriction to **Specific resources** > **Resource type**, and then select **Policy management**. For more information, see [Creating rules](/docs/iam?topic=iam-context-restrictions-create&interface=ui#context-restrictions-create-rules).

To complete any Policy Management action, a user must be assigned a role on the service with an IAM access policy and they must satisfy the context-based restrictions rule. For example, a user with the Viewer role on the IAM Access Management service can complete the action `iam.policy.read` if they send the request from the correct network zone and satisfy the rule. If the same user tries to create a policy, they can't complete that request even though they satisfy the rule because they aren't an Administrator.
{: note}

### Restricting the ability to view insights in the console
{: #cbr-insights-ui}
{: ui}

You can protect the ability to view insights, like the Inactive identities and Inactive policies reports, by scoping a rule to the `insights` resource type. Creating a rule that is scoped to the `insights` resource type protects the following actions:

- `iam-access-management.insight.get`

To configure this rule, target the **IAM Access Management service**, scope the restriction to **Specific resources** > **Resource type**, and then select **AM Insights**. For more information, see [Creating rules](/docs/iam?topic=iam-context-restrictions-create&interface=ui#context-restrictions-create-rules).


To complete any settings action, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restrictions rule. For example, a user with the Editor role on the IAM Access Management service can complete the action `iam-access-management.insight.get` if they send the request from the correct network zone and satisfy the rule. A users with the Viewer role can't complete that request even if they satisfy the rule because they aren't an Editor or Administrator.
{: note}



### Restricting the ability to manage custom roles by using the API
{: #cbr-custom-roles-api}
{: api}

You can protect the ability to manage custom roles by scoping a rule to the `customRole` resource type. Creating a rule that is scoped to the `customRole` resource type protects the following actions:

- `iam-access-management.customRole.create`
- `iam-access-management.customRole.update`
- `iam-access-management.customRole.delete`
- `iam-access-management.customRole.read`

The following example shows a rule in JSON format that protects custom role actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-access-management"
				},
				{
					"name": "resourceType",
					"value": "customRole"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

To complete any Role Management action, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restrictions rule. For example, a user with the Viewer role on the IAM Access Management service can complete the action `iam-access-management.customRole.read` if they send the request from the correct network zone and satisfy the rule. If the same user tries to create a custom role, they can't complete that request even though they satisfy the rule because they aren't an Administrator..
{: note}


### Restricting the ability to manage policies by using the API
{: #cbr-policies-api}
{: api}

You can protect the ability to manage IAM policies by scoping a rule to the `policy` resource type. Creating a rule that is scoped to the `Policy Management` resource type protects the following actions:

- `iam.delegationPolicy.create`
- `iam.delegationPolicy.update`
- `iam.policy.read`
- `iam.policy.create`
- `iam.policy.update`
- `iam.policy.delete`
- `iam.service.read`
- `iam.role.read`
- `iam.role.assign`

The following example shows a rule in JSON format that protects policy actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-access-management"
				},
				{
					"name": "resourceType",
					"value": "policy"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}



### Restricting the ability to view insights by using the API
{: #cbr-insights-api}
{: api}

You can protect the ability to view insights, like the Inactive identities and Inactive policies reports, by scoping a rule to the `insights` resource type. Creating a rule that is scoped to the `insights` resource type protects the following actions:

- `iam-access-management.insight.get`

The following example shows a rule in JSON format that protects policy actions:

```json
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "8293c49bc2724a07999910b1da94c4d6"
				},
				{
					"name": "serviceName",
					"value": "iam-access-management"
				},
				{
					"name": "resourceType",
					"value": "insight"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

To complete any settings action, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restrictions rule. For example, a user with the Editor role on the IAM Access Management service can complete the action `iam-access-management.insight.get` if they send the request from the correct network zone and satisfy the rule. A users with the Viewer role can't complete that request even if they satisfy the rule because they aren't an Editor or Administrator.
{: note}


## Protecting the IAM Identity service
{: #cbr-iam-identity}

The IAM Identity service includes the ability to view, update and delete service IDs, API keys, identity providers (IdPs), and trusted profiles. You can also assign access to service IDs and trusted profiles. All users can create service IDs, so the service actions apply to service IDs, API keys, and IdPs within the account created by other users.

You can protect the whole service, or restrict a specific set of actions based on the context of the request. To protect only a specific set of actions, review the following sections.

The IAM Token API is not subject to context-based restrictions. Any rules that target the IAM Identity service are not enforced on the Token API. The Token API uses a different mechanism to set IP address restrictions for users logging in to an account, during which users aquire a token. For more information, see [Allowing specific IP addresses for an account](/docs/iam?topic=iam-ips&interface=ui#ips_account).
{: important}

### Restricting the ability to manage service IDs and their API keys in the console
{: #iam-identity-serviceid-ui}
{: ui}

You can protect the ability to manage service IDs and their API keys by scoping a rule to the `serviceid` resource type. Creating a rule that is scoped to the `serviceid` resource type protects the following actions:

- `iam-identity.serviceid.get`
- `iam-identity.serviceid.update`
- `iam-identity.serviceid.delete`
- `iam-identity.apikey.manage`
- `iam-identity.apikey.get`
- `iam-identity.apikey.list`
- `iam-identity.apikey.create`
- `iam-identity.apikey.update`
- `iam-identity.apikey.delete`

To configure this rule, target the **IAM Identity service**, scope the rule to **Specific resources**, and select the `Resource type` attribute. Then, enter the value `serviceid`. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

### Restricting the ability to manage service IDs and their API keys by using the API
{: #iam-identity-serviceid-api}
{: api}

You can protect the ability to manage service IDs and their API keys by scoping a rule to the `serviceid` resource type. Creating a rule that is scoped to the `serviceid` resource type protects the following actions:

- `iam-identity.serviceid.get`
- `iam-identity.serviceid.update`
- `iam-identity.serviceid.delete`
- `iam-identity.apikey.manage`
- `iam-identity.apikey.get`
- `iam-identity.apikey.list`
- `iam-identity.apikey.create`
- `iam-identity.apikey.update`
- `iam-identity.apikey.delete`

The following example shows a rule in JSON format that protects `serviceid` resource type actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-identity"
				},
				{
					"name": "resourceType",
					"value": "serviceid"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

### Restricting the ability to manage user API keys in the console
{: #iam-identity-apikey-ui}
{: ui}

You can protect the ability to manage user API keys by scoping a rule to the `apikey` resource type. Creating a rule that is scoped to the `apikey` resource type protects the following actions:

- `iam-identity.apikey.manage`
- `iam-identity.apikey.get`
- `iam-identity.apikey.list`
- `iam-identity.apikey.create`
- `iam-identity.apikey.update`
- `iam-identity.apikey.delete`

To configure this rule, target the **IAM Identity service**, scope the rule to **Specific resources**, and select the `Resource type` attribute. Then, enter the value `apikey`. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

### Restricting the ability to manage user API keys by using the API
{: #iam-identity-apikey-api}
{: api}

You can protect the ability to manage user API keys by scoping a rule to the `apikey` resource type. Creating a rule that is scoped to the `apikey` resource type protects the following actions:

- `iam-identity.apikey.manage`
- `iam-identity.apikey.get`
- `iam-identity.apikey.list`
- `iam-identity.apikey.create`
- `iam-identity.apikey.update`
- `iam-identity.apikey.delete`

The following example shows a rule in JSON format that protects `apikey` resource type actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-identity"
				},
				{
					"name": "resourceType",
					"value": "apikey"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

### Restricting the ability to manage trusted profiles in the console
{: #iam-identity-profile-ui}
{: ui}

You can protect the ability to manage trusted profiles by scoping a rule to the `profile` resource type. Creating a rule that is scoped to the `profile` resource type protects the following actions:

- `iam-identity.profile.create`
- `iam-identity.profile.update`
- `iam-identity.profile.delete`
- `iam-identity.profile.get`
- `iam-identity.profile.get_session`
- `iam-identity.profile.revoke_session`
- `iam-identity.profile.linkToResource`

To configure this rule, target the **IAM Identity service**, scope the rule to **Specific resources**, and select the `Resource type` attribute. Then, enter the value `profile`. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

### Restricting the ability to manage trusted profiles by using the API
{: #iam-identity-profile-api}
{: api}

You can protect the ability to manage trusted profiles by scoping a rule to the `profile` resource type. Creating a rule that is scoped to the `profile` resource type protects the following actions:

- `iam-identity.profile.create`
- `iam-identity.profile.update`
- `iam-identity.profile.delete`
- `iam-identity.profile.get`
- `iam-identity.profile.get_session`
- `iam-identity.profile.revoke_session`
- `iam-identity.profile.linkToResource`

The following example shows a rule in JSON format that protects `profile` resource type actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-identity"
				},
				{
					"name": "resourceType",
					"value": "profile"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

### Restricting the ability to manage account settings in the console
{: #iam-identity-settings-ui}
{: ui}

You can protect the ability to manage account settings by scoping a rule to the `settings` resource type. Creating a rule that is scoped to the `settings` resource type protects the following actions:

- `iam-identity.account.get`
- `iam-identity.account.create`
- `iam-identity.account.update`
- `iam-identity.account.create`
- `iam-identity.account.update`
- `iam-identity.account.enable_idp`
- `iam-identity.account.disable_idp`
- `iam-identity.account.delete`
- `iam-identity.session.manage`

To configure this rule, target the **IAM Identity service**, scope the rule to **Specific resources**, and select the `Resource type` attribute. Then, enter the value `settings`. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

### Restricting the ability to manage account settings by using the API
{: #iam-identity-settings-api}
{: api}

You can protect the ability to manage account settings by scoping a rule to the `settings` resource type. Creating a rule that is scoped to the `settings` resource type protects the following actions:

- `iam-identity.account.get`
- `iam-identity.account.create`
- `iam-identity.account.update`
- `iam-identity.account.create`
- `iam-identity.account.update`
- `iam-identity.account.enable_idp`
- `iam-identity.account.disable_idp`
- `iam-identity.account.delete`
- `iam-identity.session.manage`

The following example shows a rule in JSON format that protects `settings` resource type actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-identity"
				},
				{
					"name": "resourceType",
					"value": "settings"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

### Restricting the ability to manage Identity Providers in the console
{: #iam-identity-ipd-ui}
{: ui}

You can protect the ability to manage Identity Providers (IdPs) by scoping a rule to the `idp` resource type. Creating a rule that is scoped to the `ipd` resource type protects the following actions:

- `iam-identity.idp.get`
- `iam-identity.idp.list`
- `iam-identity.idp.create`
- `iam-identity.idp.update`
- `iam-identity.idp.delete`
- `iam-identity.idp.test`
- `iam-identity.idp.metadata`

To configure this rule, target the **IAM Identity service**, scope the rule to **Specific resources**, and select the `Resource type` attribute. Then, enter the value `idp`. For more information about the steps to set up a rule, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).

### Restricting the ability to manage Identity Providers by using the API
{: #iam-identity-ipd-api}
{: api}

You can protect the ability to manage Identity Providers (IdPs) by scoping a rule to the `idp` resource type. Creating a rule that is scoped to the `idp` resource type protects the following actions:

- `iam-identity.idp.get`
- `iam-identity.idp.list`
- `iam-identity.idp.create`
- `iam-identity.idp.update`
- `iam-identity.idp.delete`
- `iam-identity.idp.test`
- `iam-identity.idp.metadata`

The following example shows a rule in JSON format that protects `idp` resource type actions:

```bash
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "iam-identity"
				},
				{
					"name": "resourceType",
					"value": "idp"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
```
{: curl}
{: codeblock}

## Protecting the User Management service
{: #cbr-user-management}

The User Management service includes the ability to view users in an account, invite and remove users, and view and update user profile settings. You can create a rule that protects all actions associated with this service.

The viewer role on the User Management service is commonly assigned for users assigned a role to view or manage support cases. If an account owner restricts the visibility of the user list in the IAM settings, users can't see support cases that are opened by other users in the account. However, if they are assigned the viewer role for the user management service, the user list visibility setting doesn't affect the ability to view cases in the account.
{: tip}

To configure this rule, target the **User Management service**. For more information about the steps to set up a rule in the console, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).
{: ui}

The following example shows a rule in JSON format that protects all `user-management` actions:
{: api}

```bash
{
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "serviceName",
					"value": "user-management"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
}
```
{: curl}
{: codeblock}
{: api}

## Protecting All IAM Account Management services
{: #cbr-iam-all}

**All IAM Account Management services** is the grouping of a subset of account management services, which includes IAM Identity, IAM Access Management, IAM User Management, and IAM Groups. You can create a rule that protects all actions associated with these services.

To configure this rule, target the **All IAM Account Management services**. For more information about the steps to set up a rule in the console, see [How IAM integrates with context-based restrictions](/docs/iam?topic=iam-iam-services-cbr&interface=ui#iam-cbr-overview).
{: ui}

The following example shows a rule in JSON format that protects all actions associated with the  `IAM` service grouping:
{: api}

```bash
{
{
	"resources": [
		{
			"attributes": [
				{
					"name": "accountId",
					"value": "alphanumericAccoutnID"
				},
				{
					"name": "service_group_id",
					"value": "IAM"
				}
			]
		}
	],
	"description": "",
	"contexts": [],
	"enforcement_mode": "enabled"
}
}
```
{: curl}
{: codeblock}
{: api}
