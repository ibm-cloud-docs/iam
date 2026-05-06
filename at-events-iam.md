---

copyright:

  years: 2024, 2026
lastupdated: "2026-05-06"

keywords: activity tracking, IAM events, Identity and Access Management, observibility

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}



# Activity tracking events for IAM
{: #at_events_iam}



{{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) generates activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations-iam}



IAM sends activity tracking events by {{site.data.keyword.atracker_full_notm}} to the Frankfurt (`eu-de`) region.











### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone-iam}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}}.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

### Viewing activity tracking events for IAM
{: #at-viewing-iam}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

The IAM service generates [global activity tracking events](/docs/atracker?topic=atracker-event_types#event_types_global) for the actions that are listed in this document. Select `Platform events (global)` as the location to send audit events from when you configure an {{site.data.keyword.atracker_full_notm}} route.
{: tip}

To view IAM events in the {{site.data.keyword.logs_full_notm}} dashboard, go to the **Subsystems** filter and select the values with the prefix `iam-`. For example, `iam-am`, `iam-identity`, or `iam-groups`.

## Access groups events
{: #at_events_iam_access}

### Account events
{: #at_events_iam_access_account}

The following table lists the actions that generate an event:

| Action                      | Description |
|-----------------------------|-------------|
| `iam-groups.account-settings.read` | An event is generated when an initiator views the account settings for the access groups service. |
| `iam-groups.account-settings.update` | An event is generated when an initiator updates their account settings for the access groups service. |
{: caption="Events that are generated for access groups" caption-side="bottom"}

### Access groups events
{: #at_events_iam_access_groups}

The following table lists the actions that generate an event:

| Action                      | Description |
|-----------------------------|-------------|
| `iam-groups.group.create`   | An event is generated when an initiator creates an access group. |
| `iam-groups.group.read`     | An event is generated when an initiator views an access group. |
| `iam-groups.group.update`   | An event is generated when an initiator updates a group name or a description. |
| `iam-groups.group.delete`   | An event is generated when an initiator deletes an access group. |
| `iam-groups.groups.list`    | An event is generated when an initiator views the access groups. |
{: caption="Events that are generated for access groups" caption-side="bottom"}

### Members events
{: #at_events_iam_access_members}

The following table lists the actions that generate an event:

| Action                      | Description |
|-----------------------------|-------------|
| `iam-groups.federated-member.add` | An event is generated when an initiator logs in to the account and gains federated membership to an access group. |
| `iam-groups.member.add`     | An event is generated when an initiator adds a member to an access group. |
| `iam-groups.member.delete`  | An event is generated when an initiator removes a member from an access group. |
| `iam-groups.member.read`    | An event is generated when an initiator views a member's membership. |
|`iam-groups.members.list`    | An event is generated when an initiator views the members for an access group. |
{: caption="Events that are generated for access groups" caption-side="bottom"}

### Rules events
{: #at_events_iam_access_rules}

The following table lists the actions that generate an event:

| Action                      | Description |
|-----------------------------|-------------|
| `iam-groups.rule.read`      | An event is generated when an initiator views a rule in an access group. |
| `iam-groups.rule.create`    | An event is generated when an initiator adds a rule to an access group. |
| `iam-groups.rule.update`    | An event is generated when an initiator modifies the rule name. |
| `iam-groups.rule.delete`    | An event is generated when an initiator deletes a rule from an access group. |
| `iam-groups.rules.list`     | An event is generated when an initiator views the rules for an access group. |
{: caption="Events that are generated for access groups" caption-side="bottom"}

## Trusted profiles events
{: #at_events_iam_profiles}

The following table lists the actions that generate an event:

| Action                      | Description |
|-----------------------------|-------------|
| `iam-identity.account-profile.create`  | An event is generated when an initiator creates a trusted profile. |
| `iam-identity.account-profile.update`   | An event is generated when an initiator updates a trusted profile. |
| `iam-identity.account-profile.delete`   | An event is generated when an initiator deletes a trusted profile. |
{: caption="Events that are generated for trusted profiles" caption-side="bottom"}

## Policy events
{: #at_events_iam_policies}

The following table lists the actions that generate an event:

| Action                 | Description |
|------------------------|---------|
| `iam-am.policy.create` | An event is generated when an initiator adds a policy to a user or access group. |
| `iam-am.policy.update` | An event is generated when an initiator modifies permissions to a policy of a user or access group.|
| `iam-am.policy.delete` | An event is generated when an initiator deletes a policy that is assigned to a user or access group. |
{: caption="Events that are generated for policy actions" caption-side="bottom"}

## Service ID events
{: #at_events_iam_serviceids}

The following table lists the actions that generate an event:

| Action | Description |
|----------|---------|
| `iam-identity.account-serviceid.create` | An event is generated when an initiator creates a service ID.  |
| `iam-identity.account-serviceid.update` | An event is generated when an initiator renames a service ID or modifies its description. |
| `iam-identity.account-serviceid.delete` | An event is generated when an initiator deletes a service ID. |
{: caption="Events that are generated for service IDs actions" caption-side="bottom"}

## API key events
{: #at_events_iam_apikeys}

The following table lists the actions that generate an event:

| Action | Description |
|----------|---------|
| `iam-identity.user-apikey.create`      | An event is generated when an initiator creates an API key. |
| `iam-identity.user-apikey.update`      | An event is generated when an initiator renames an API key or modifies its description. |
| `iam-identity.user-apikey.delete`      | An event is generated when an initiator deletes an API key. |
| `iam-identity.serviceid-apikey.create` | An event is generated when an initiator creates an API key for a service ID. |
| `iam-identity.serviceid-apikey.delete` | An event is generated when an initiator deletes an API key for a service ID. |
| `iam-identity.serviceid-apikey.update` | An event is generated when an initiator renames an API key for a service ID or modifies its description. |
{: caption="Events that are generated for API keys actions" caption-side="bottom"}


## Login and logout events
{: #at_events_iam_login}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `iam-identity.user-apikey.login`         | An event is generated when a user logs in to the {{site.data.keyword.cloud_notm}} by using an API key. |
| `iam-identity.serviceid-apikey.login`    | An event is generated when an initiator logs in to the {{site.data.keyword.cloud_notm}} by using an API key that is associated with a service ID. |
| `iam-identity.user-identitycookie.login` | This is an event that is generated when an initiator requests an identity cookie to run an action. |
| `iam-identity.user-refreshtoken.login`   | This is an event that is generated when the initiator logs in to {{site.data.keyword.cloud_notm}}, or when an initiator that is already logged in requests a new refresh token to run an action. |
| `iam-identity.user-passcode.login` `iam-identity.trustedprofile-apikey.login` | This is an event that is generated when the initiator logs in to {{site.data.keyword.cloud_notm}} by applying a trusted profile, or when an initiator that is already logged in by applying a trusted profile requests a new refresh token to run an action. |
| `iam-identity.user.logout` | This is an event that is generated when the initiator logs out of the {{site.data.keyword.cloud_notm}}. |
{: caption="Events that are generated for user login and logout actions" caption-side="bottom"}

## Enterprise IAM events
{: #at_events_iam_enterprise}

### Policy tempalte events
{: #at_events_iam_enterprise_policy}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `iam-access-management.policy-template.create` | An event is generated when a user creates an enterprise-managed IAM policy template. |
| `iam-access-management.policy-template.update`    | An event is generated when a user updates an enterprise-managed IAM policy template. |
| `iam-access-management.policy-template.delete`  | An event is generated when a user deletes an enterprise-managed IAM policy template. |
| `iam-access-management.policy-template.read` | An event is generated when a user reads an enterprise-managed IAM policy template. |
| `iam-access-management.policy-assignment.create`    | An event is generated when a user assigns an enterprise-managed IAM policy template to child accounts. |
| `iam-access-management.policy-assignment.update` | An event is generated when a user updates an enterprise-managed IAM policy template assignment. |
| `iam-access-management.policy-assignment.delete` | An event is generated when a user deletes an enterprise-managed IAM policy template assignment. |
| `iam-access-management.policy-assignment.read` | An event is generated when a user reads an enterprise-managed IAM policy template assignment. |
{: caption="Events that are generated for enterprise-managed IAM policy template actions" caption-side="bottom"}

### Access group tempalte events
{: #at_events_iam_enterprise_groups}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `iam-groups.groups-template.create` | An event is generated when a user creates an enterprise-managed IAM access group template. |
| `iam-groups.groups-template.delete` | An event is generated when a user deletes an enterprise-managed IAM access group template. |
| `iam-groups.groups-template.update`| An event is generated when a user updates an enterprise-managed IAM access group template. |
| `iam-groups.groups-template.read` | An event is generated when a user reads an enterprise-managed IAM access group template. |
| `iam-groups.groups-template.assign` | An event is generated when a user assigns an enterprise-managed IAM access group template to child accounts. |
| `iam-groups.groups-template.remove` | An event is generated when a user removes an enterprise-managed IAM access group template assignment. |
| `iam-groups.groups-template.assignment-read` | An event is generated when a user reads an enterprise-managed IAM access group template assignment. |
| `iam-groups.groups-template.assignment-update` | An event is generated when a user updates an enterprise-managed IAM access group template assignment. |
{: caption="Events that are generated for user enterprise-managed IAM access group template actions" caption-side="bottom"}

### Trusted profile tempalte events
{: #at_events_iam_enterprise_tp}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `iam-identity.profile-template.create` | An event is generated when a user creates an enterprise-managed IAM trusted profile template. |
| `iam-identity.profile-template.delete` | An event is generated when a user deletes an enterprise-managed IAM trusted profile template. |
| `iam-identity.profile-template.update` | An event is generated when a user updates an enterprise-managed IAM trusted profile template. |
| `iam-identity.profile-template.read` | An event is generated when a user reads an enterprise-managed IAM trusted profile template. |
| `iam-identity.profile-template.assign` | An event is generated when a user assigns an enterprise-managed IAM trusted profile template to child accounts. |
| `iam-identity.profile-template.remove` | An event is generated when a user removes an enterprise-managed IAM trusted profile template assignment. |
| `iam-identity.profile-template.assignment-read` | An event is generated when a user reads an enterprise-managed IAM trusted profile template assignment. |
| `iam-identity.profile-template.assignment-update` | An event is generated when a user updates an enterprise-managed IAM trusted profile template assignment. |
{: caption="Events that are generated for user enterprise-managed IAM trusted profile template actions" caption-side="bottom"}

### Settings tempalte events
{: #at_events_iam_enterprise_settings}

The following table lists the actions that generate an event:

| Action                                   | Description |
|------------------------------------------|---------|
| `iam-identity.account-settings-template.create` | An event is generated when a user creates an enterprise-managed IAM settings template. |
| `iam-identity.account-settings-template.delete` | An event is generated when a user deletes an enterprise-managed IAM settings template. |
| `iam-identity.account-settings-template.update` | An event is generated when a user updates an enterprise-managed IAM settings template. |
| `iam-identity.account-settings-template.read` | An event is generated when a user reads an enterprise-managed IAM settings template. |
| `iam-identity.account-settings-template.assign` | An event is generated when a user assigns an enterprise-managed IAM settings template to child accounts. |
| `iam-identity.account-settings-template.remove` | An event is generated when a user removes an enterprise-managed IAM settings template assignment. |
| `iam-identity.account-settings-template.assignment-read` | An event is generated when a user reads an enterprise-managed IAM settings template assignment. |
| `iam-identity.account-settings-template.assignment-update` | An event is generated when a user updates an enterprise-managed IAM settings template assignment. |
{: caption="Events that are generated for user enterprise-managed IAM settings template actions" caption-side="bottom"}

## Analyzing IAM activity tracking events
{: #at_events_iam_analyze}



### Login events
{: #at_events_iam_analyze_login_events}

In the {{site.data.keyword.cloud_notm}}, an administrator, or a user that has the correct access in your account, has different options to manage a user's login settings. For example, an administrator can order external authentication options, enable a one-time passcode to be used during login, enable the use of security questions at login, or set a password expiration time period. For more information, see [Types of multifactor authentication](/docs/iam?topic=iam-types).

* A user can log in by using a user ID and password.
* A federated user that uses a corporate or enterprise single sign-on ID can log in to {{site.data.keyword.cloud_notm}} from the command-line interface (CLI) by using either a one-time passcode or an API key. For more information, see [Logging in with a federated ID](/docs/iam?topic=iam-federated_id).
* A user can log in by using an API key.
* A federated user that uses a corporate or enterprise single sign-on ID can log in to {{site.data.keyword.cloud_notm}} by applying a trusted profile.

The following fields include additional information:

* The `initiator.name` includes information about the user that logs in to the account.
* The `X-Global-Transaction-Id` includes an ID that you can use when you open a support ticket if you need to get more information.

#### Log in from the {{site.data.keyword.cloud_notm}} UI
{: #at_events_iam_analyze_login_events-1}

When a user logs in from the {{site.data.keyword.cloud_notm}} UI, you get an event in the account with action `iam-identity.user-refreshtoken.login`.

The following field includes additional information:

* In requestData, the `client_id` field is set to **HOP55v1CCT**. This value indicates a UI request.

#### Log in with a federated ID from the {{site.data.keyword.cloud_notm}} CLI by using a one-time passcode or an API key
{: #at_events_iam_analyze_login_events-2}

When a user [logs in from the {{site.data.keyword.cloud_notm}} CLI by using a one-time passcode](/docs/iam?topic=iam-federated_id#onetime_passcode), you get an event in the account with action `iam-identity.user-refreshtoken.login`.

When a user [logs in from the {{site.data.keyword.cloud_notm}} CLI by using an API key](/docs/iam?topic=iam-federated_id#api_key), you get an event in the account with action `iam-identity.user-apikey.login`.

The following field includes additional information:

* In requestData, the `client_id` field is set to **bx**. This value indicates a CLI request.

#### Log in with a federated ID by using trusted profiles
{: #at_events_iam_analyze_login_events-2a}

When a user [logs in with a federated ID by using trusted profiles](/docs/iam?topic=iam-federated_id), you get an event in the account with action `iam-identity.trustedprofile-apikey.login`.

#### Failed log in actions
{: #at_events_iam_analyze_login_events-3}

When a user logs in to the {{site.data.keyword.cloud_notm}}, the user ID (IBMid) and credentiasls are validated first. At this point, the user has not selected an account. Notice that a user can belong to multiple accounts.

After the user ID is authenticated successfully in the {{site.data.keyword.cloud_notm}}, the user can choose an account. It is at this point in the process that an account is associated to the log in request, and an event with action `iam-identity.user-refreshtoken.login`, or `iam-identity.user-apikey.login` is generated in your account.

In {{site.data.keyword.atracker_full_notm}}, you can see events that are associated to your account. Failed log in actions do not generate an event that you can monitor in your account.

### Logout events
{: #at_events_iam_analyze_logout_events}

When a user logs out of the {{site.data.keyword.cloud_notm}}, the `iam-identity.user.logout` event is generated.

### Update an account service ID
{: #at_events_iam_analyze_update_acc_scvid}

A service ID identifies a service or application similar to how a user ID identifies a user.

When an action to update a service ID is requested, you get an event in the account with action `iam-identity.account-serviceid.update`.

The following fields include additional information:

* The `initiator.name` field includes information about who has requested to update the service ID.
* The `target.name` field includes information about the service ID that is changed.
* The `initiator.host.agent` field indicates if the request comes from the UI or the CLI. When the field is set to **Not Set**, the request originates in the UI. When the field is set to **{{site.data.keyword.cloud_notm}} CLI**, the request originates at the command line.

#### Lock and unlock a service ID
{: #at_events_iam_analyze_update_acc_scvid_1}

The following field includes additional information:

* In requestData, the `lock` field is set to **true** when the service ID is locked, and to **false** when it is unlocked.

#### Add or modify a description
{: #at_events_iam_analyze_update_acc_scvid_2}

When a request to change a description generates an event, the following fields include information that can help you determine this action:

* In requestData, the `lock` field is set to **false**.
* In requestData, the `prev_instance_name` field and the `instance_name` field are set to the same value.

#### Change the name of a service ID
{: #at_events_iam_analyze_update_acc_scvid_3}

The following fields include additional information:

* In requestData, the `lock` field is set to **false**.
* In requestData, the `instance_name` field includes the new name of the API key.
* In requestData, the `prev_instance_name` field includes the name of the API key before it was changed.

### Limits events
{: #at_events_iam_limits}

There are [limitations](/docs/iam?topic=iam-cloudaccess#iam_limits) on the number of service IDs, API keys, trusted profiles, and policies allowed in an account. An event is generated when your account reaches 90% of the of the limit for service IDs, API keys, trusted profiles, and policies.

The following is an example message when an account is approaching the maximum number of service IDs:

> Warning: You have reached 90% of the maximum number of allowed Service IDs in account 10t2tyv8d1f88940dfc56af370b1f109. Your current count is 1800 and the limit is 2000. Reduce the number of Service IDs before you hit the limit to ensure that you are not blocked from creating new Service IDs.

Apply the following search query to view all limits events:
- `the maximum number of allowed`

Start by removing inactive identities if they are no longer needed. For more information, see [Identifying inactive identities](/docs/iam?topic=iam-id-inactive-identities).
{: tip}

### Update a user API key or a service ID API key
{: #at_events_iam_update_apikey}

When an action to update an API key is requested, you get an event in the account with one of the following actions:

* To update a user API key, the action is `iam-identity.user-apikey.update`.
* To update a service ID API key, the action is `iam-identity.account-serviceid.update`.

The following fields include additional information:

* The `initiator.name` field includes information about who has requested to update the API key.
* The `target.name` field includes information about the API key that is changed.
* The `initiator.host.agent` field indicates if the request comes from the UI or the CLI. When the field is set to **Not Set**, the request originates in the UI. When the field is set to **{{site.data.keyword.cloud_notm}} CLI**, the request originates at the command line.

#### Lock and unlock a service ID
{: #at_events_iam_update_apikey_1}

The following field includes additional information:

* In requestData, the `lock` field is set to **true** when the API key is locked, and to **false** when it is unlocked.

#### Add or modify a description
{: #at_events_iam_update_apikey_2}

When a request to change a description generates an event, the following fields include information that can help you determine this action:

* In requestData, the `lock` field is set to **false**.
* In requestData, the `prev_instance_name` field and the `instance_name` field are set to the same value.

#### Change the name of a service ID
{: #at_events_iam_update_apikey_3}

The following fields include additional information:

* In requestData, the `lock` field is set to **false**.
* In requestData, the `instance_name` field includes the new name of the API key.
* In requestData, the `prev_instance_name` field includes the name of the API key before it was changed.

## Analyzing events that fail
{: #at_events_iam_analyze_fail}

### Initiator not authorized. Request to update an API key or service ID fails
{: #an_fail_not_authorized}

For example, when a user logs into your account using an API key, the user is authenticated to access your account. However, this API key may not have permissions to run actions to modify API keys or service IDs in the account. When this happens, you get one of the following messages:

* **IAM Identity Service: update user-apikey APIKeyName -failure**
* **IAM Identity Service: update account-serviceid ServiceIDName -failure**

To look for information about the user that has requested a change to an API key or to a service ID, look at the initiator fields in the event.

When a user does not have permissions to run this action in your account, you get a failure event:

* The `initiator.name` field is empty. This information is not available at the time the event is generated.
* The user ID has been authenticated in your {{site.data.keyword.cloud_notm}} account.
* The action targets your account.
* The user ID is not authorized to run this action in your account.

To find out the user who has tried to modify an API key or a service ID, complete the following steps:

1. Copy the value of the `initiator.id`. This field includes the ID of the user that is trying to run this action in your account.
2. Get the email address that is associated with the user. To complete this step, you must have administrator permissions in the account. Run the following command:

    ```json
   ibmcloud account users --output json | grep -A 1 InitiatorID
    ```
    {: codeblock}

   Where InitiatorID is the value of the field `initiator.id`, and has the format IBMid-XXXXXXXXXX.

   The output of this command returns 2 fields. The `ibmUniqueId` field shows the ID of the user that matched the event `initiator.name` field. The `email` field shows the email address associated with that ID.

To get the API key on which the action has been requested and failed, see the field `prev_instance_name` in requestData.

### Resource is locked. Request to update Service ID or API key fails
{: #an_fail_locked}

When a service ID or an API key are locked, you cannot change any of its attributes. The event that is generated has an `outcome` of **failure**.

Depending on the resource type, you can get any of the following messages:

* Service ID: The message that you get says **IAM Identity Service: update account-serviceid ServiceIDName -failure** where *ServiceIDName* is the name of the service ID.
* User API key: The message that you get says **IAM Identity Service: update user-apikey APIkeyName -failure** where *APIkeyName* is the name of the API key.
* Account API key: The message that you get says **IAM Identity Service: update account-apikey APIkeyName -failure** where *APIkeyName* is the name of the API key.

In the event, the `lock` field in requestData is set to **true**. This is the reason why this action fails. To successfully change an attribute of a service ID, the `lock` field must be set to **false**.

Notice that the field `severity` is set to **critical**. Someone is trying to modify a service ID that is locked in the account.
