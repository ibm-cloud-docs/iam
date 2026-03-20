---

copyright:

  years: 2017, 2026
lastupdated: "2026-03-20"

keywords: service ID, create service ID, lock service ID, service ID example

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Creating and working with service IDs
{: #serviceids}

A service ID identifies a service or application similar to how a user ID identifies a user. You can create a service ID and use it to enable an application outside of {{site.data.keyword.cloud_notm}} access to your {{site.data.keyword.cloud_notm}} services. You can assign specific access policies to the service ID that restrict permissions for using specific services, or even combine permissions for accessing different services. Since service IDs are not tied to a specific user, if a user leaves an organization and is deleted from the account, the service ID remains. This way, your application or service stays up and running.
{: shortdesc}

When you create a service ID, you create a unique name and description that is easy for you to identify and work with in the console. After you create your service ID, you can [create API keys](/docs/account?topic=account-serviceidapikeys#create_service_key) specific to each service ID that your application can use to authenticate with your {{site.data.keyword.cloud_notm}} services. To ensure that your application has the appropriate access for authenticating with your {{site.data.keyword.cloud_notm}} services, you use access policies that are assigned to each service ID that you create.

The access policies that are associated with a service ID enable specific actions that can be taken when that service ID is used to access a specific service. A service ID can have multiple policies assigned to it for different Identity and access-enabled services, and even different instances of a single service. For example, you have two services with two service instances each. You might assign the Viewer role for all available instances of one service and assign the Editor role for only one instance of a second service. This way, you can customize access to multiple services, but use a single API key for authentication to all.

All users have access to create a service ID in an account to which they are a member. However, to allow a user in an account access to view or manage a service ID that they did not personally create, they must have access with a role on the IAM Identity account management service. For more information, see [IAM Identity service](/docs/account?topic=account-account-services#identity-service-account-management).

Service ID groups organize service IDs more effectively into groups, improving the efficiency of listing operations by reducing the number of service IDs that need to be processed. Service ID groups don't integrate with access management, so they cannot be used in IAM policies to control access.

You can assign any identity access to view or manage a service ID by using access management tags. For more information, see [Attaching tags to a service ID](/docs/account?topic=account-attaching-and-detaching-tags-on-a-resource&interface=ui#am-tags-serviceid-ui).
{: tip}

If **Restrict service ID creation** is enabled in your IAM account settings, then everyone in the account, including account owners, is blocked from creating service IDs unless they are assigned explicit access. For more information, see [Restricting users from creating service IDs](/docs/account?topic=account-restrict-service-id-create).
{: important}

## Creating a service ID by using the console
{: #create_serviceid}
{: ui}

When you create a service ID, it must be added to a service ID group. The default group is created for you automatically, but you can [create more groups](/docs/account?topic=account-serviceids&interface=ui#create-group-ui) if you need to. If you don't create any other groups, service IDs are added to the default group. To create a service ID, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
1. (Optional) Select a group from the **Service ID group** menu. The default group is selected for you. You can't move a service ID to another group, so make sure that the correct group is selected before you create the service ID. 
1. Click **Create**.
1. Follow the process to create a name and description for your service ID.
1. Click **Create**.

## Creating a service ID by using the CLI
{: #create_serviceid-cli}
{: cli}

Service ID groups help you when you encounter a limit on the number of service IDs allowed in an account. Instead of increasing these limits, which might lead to performance issues, Service ID groups provide a way to create more service IDs without impacting system performance.

When you create a service ID, it must be added to a service ID group. The default group is created for you automatically, but you can create more groups if you need to. If you don't specify a service ID group, your service ID is added to the default group.

You can't move a service ID to another group, so make sure that the correct group is specified in the command before you create the service ID. 
{: important}

To create a service ID, use the [**`ibmcloud iam service-id-create`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id_create) command.

## Creating a service ID by using the API
{: #create_serviceid-api}
{: api}

Service ID groups help you when you encounter a limit on the number of service IDs allowed in an account. Instead of increasing these limits, which might lead to performance issues, Service ID groups provide a way to create more service IDs without impacting system performance.

When you create a service ID, it must be added to a service ID group. The default group is created for you automatically, but you can create more groups if you need to. If you don't specify a service ID group, your service ID is added to the default group.

You can't move a service ID to another group, so make sure that the correct group is specified in the API before you create the service ID. 
{: important}

To create a service ID, use the [Create a service ID API method](/apidocs/iam-identity-token-api#create-service-id).

## Managing a service ID by using the console
{: #update_serviceid}
{: ui}

You can edit a service ID by changing the name and description at any time. You can also delete and create new API keys as needed, update the assigned access policies, or delete the service ID. 

You can't move a service ID to another service ID group. Instead, delete the service ID and create another one in the service ID group you want to use. 
{: tip}

Any changes that you make to an existing service ID, such as changing the assigned policies or deleting an API key that is used, might cause service interruptions to applications that use that service ID. Deleting a service ID also deletes all associated API keys and assigned policies. This action can't be undone, and might cause disruptions between dependent services.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
1. (Optional) Select a group from the **Service ID group** menu. The default group is selected for you. 
1. Hover on the row of a service ID and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to manage your service ID.

To quickly assign access or create API keys, click the name of the service ID in the row. For more information about working with API keys, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).
{: tip}

## Managing a service ID by using the CLI
{: #update_serviceid-cli}
{: cli}

You can use the CLI to view details of a service ID, update the name and description, delete a service ID, and more.

- To view details of a service ID, use the [**`ibmcloud iam service-id`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id) command.
- To update the name and description of a service ID, use the [**`ibmcloud iam service-id-update`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id_update) command.
- To delete a service ID, use the [**`ibmcloud iam service-id-delete`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id_delete) command.

   Deleting a service ID also deletes all associated API keys and assigned policies. This action can't be undone, and might cause disruptions between dependent services.
   {: important}

For a full list of service ID commands, parameters, and examples go to the [IAM CLI documentation](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli).

## Managing a service ID by using the API
{: #update_serviceid-api}
{: api}

You can use the API to view details of a service ID, update the name and description, delete a service ID, and more. 
- To view details of a service ID, use the [Update service ID](/apidocs/iam-identity-token-api#update-service-id) API method. 
- To update the name and description of a service ID, use the [Update service ID](/apidocs/iam-identity-token-api#update-service-id) API method. 
- To delete a service ID, use the [Delete a service ID and associated API keys](/apidocs/iam-identity-token-api#delete-service-id) API method. 

   Deleting a service ID also deletes all associated API keys and assigned policies. This action can't be undone, and might cause disruptions between dependent services.
   {: important}

For a full list of service ID methods, optional and required request parameters, and examples go to the [IAM Identity Services API documentation](/apidocs/iam-identity-token-api#list-service-ids).

## Locking a service ID
{: #lock_serviceid}

To avoid a situation where your service ID is deleted causing an outage or disruption for the users of your service, you can lock your service ID. Locking a service ID also prevents any policies from being changed, deleted, or assigned. In addition to the ability to lock a service ID, you can [lock individual API keys](/docs/account?topic=account-serviceidapikeys#lockkey) that are associated with each service ID that you create in your account.

While locked service IDs cannot be deleted from the account and the access policies can't be updated, locked service IDs can still be removed from any access group that they are added to. This means that any access that is assigned to the ID by its membership in an access group is removed when the service ID is removed from the access group.
{: note}

### Providing user access for locking and unlocking service IDs
{: #access_lock_serviceid}

In order for a user to have access to lock and unlock service IDs and API keys that are associated with service IDs, they must be assigned a specific access policy. Two types of access policies can grant the proper access: access to all service IDs in the account or access to a specific service ID in the account

To assign access to all service IDs in the account, set an access policy for account management services with the following details:

* Editor or Administrator role
* IAM Identity Service

To assign access to a specific service ID in the account, set an access policy for account management services with the following details:

* Editor or Administrator role
* IAM Identity Service
* Specify `serviceid` in the Resource type field
* Specify the service ID identifier in the Resource ID field

To get the identifier of a specific service ID, go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select **Service IDs**. Select the service ID that you want to view details for, and copy the ID value.
{: ui}

### Locking and unlocking a service ID by using the console
{: #lock_serviceid_ui}
{: ui}

You must have the appropriate level of access to lock or unlock a service ID. To lock or unlock a service ID, complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)** and then select **Service IDs**. 
1. Hover on the row of a service ID and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to lock or unlock a service ID. 

### Locking and unlocking a service ID by using the CLI
{: #lock_serviceid_cli}
{: cli}

- To lock a service ID, use the [**`ibmcloud iam service-id-lock`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id_lock) command.
- To unlock a service ID, use the [**`ibmcloud iam service-id-unlock`**](/docs/account?topic=account-ibmcloud_commands_iam&interface=cli#ibmcloud_iam_service_id_unlock) command.

You must have the appropriate level of access to unlock a service ID.
{: remember}

### Locking and unlocking a service ID by using the API
{: #lock_serviceid_api}
{: api}

- To lock a service ID, use the [Lock the service ID](/apidocs/iam-identity-token-api#lock-service-id) API method. 
- To unlock a service ID, use the [Unlock the service ID](/apidocs/iam-identity-token-api#unlock-service-id) API method. 

You must have the appropriate level of access to unlock a service ID.
{: remember}

## Creating and working with service ID groups by using the console 
{: #create-and-work-with-groups-ui}
{: ui}

When you create a service ID, it must be added to a service ID group. The default group is created for you automatically, but you can create more groups if you need to. Each service ID group can contain up to 2,000 service IDs, with a maximum limit of 100,000 service IDs in your account. 

### Creating a service ID group by using the console 
{: #create-group-ui}
{: ui}

To create a service ID group, complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
1. Click **Create group**.
1. Follow the process to create a name and description for your service ID group.
1. Click **Create**.

### Deleting a service ID group by using the console 
{: #delete-group-ui}
{: ui}

To delete a service ID group, it must be empty. Delete all service IDs within the group before you delete the group. Then, complete the following steps: 

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
1. Select a group from the **Service ID group** menu. 
   
   The default service ID group can't be deleted. 
   {: important}

1. Click **Delete** in the table header. 
1. Click **Delete** to confirm. 

## Creating and working with service ID groups by using the CLI
{: #create-and-work-with-groups-cli}
{: cli}

You can create and manage service ID groups by using the console. To see the steps, switch to the UI instructions.

## Creating and working with service ID groups by using the API
{: #create-and-work-with-groups-api}
{: api}

You can create and manage service ID groups by using the console. To see the steps, switch to the UI instructions.
