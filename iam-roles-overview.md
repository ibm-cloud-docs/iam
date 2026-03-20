---

copyright:

  years: 2015, 2026
lastupdated: "2026-03-20"

keywords: IAM access, access policy, IAM roles, platform management roles, service access roles, types of access policies, custom roles, permissions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Platform and service access roles for permissions
{: #userroles}

Define user permissions with platform management roles and service access roles. Create custom roles to meet your organization's specific needs.
{: shortdesc}

All services that are organized in a resource group in your account are managed by using {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Account owners are automatically assigned the account administrator role. As the account administrator, you can assign and manage access for users, create resource groups, create access groups, create trusted profiles, view billing details and track usage, and create service instances. You provide access for users, service IDs, access groups, and trusted profiles by creating policies that set a target for the subject of the policy to access and a role that defines what type of access that is allowed.

## IAM roles
{: #iamusermanrol}

You can manage and define access based on specific roles for users and resources in your account.

* Platform management roles cover a range of actions, including the ability to create and delete instances, manage credentials, and manage access. The platform roles are administrator, editor, operator, viewer. Platform management roles also apply to [account management services](/docs/account?topic=account-account-services&interface=ui#account-management-actions-roles) that enable users to invite users, manage service IDs, access policies, catalog entries, and track billing and usage depending on their assigned role on an account management service.

* Service access roles define a user or service’s ability to perform actions on a service instance, such as accessing the console or performing API calls. The most common service access roles are manager, writer, and reader. Each service maps particular actions for working with the service to each of these roles.

   You might not see all of the roles that are listed here as options when you assign policies in the UI because only the roles available for the service that you chose are displayed. For more information on what roles are enabled and what actions each access role allows for each service, see the documentation for that service.
   {: note}

* Custom roles for a service can be created on the IAM Roles page by the account owner or a user assigned the administrator role on the role management service.

   You can review the available roles and associated actions for a particular service by going to the [Roles](https://cloud.ibm.com/iam/roles){: external} page, and selecting the service that you want to learn more about. This is the same page where you can create a custom role in the console.
   {: note}

### Platform management roles
{: #platformroles}

With platform management roles, users can be assigned varying levels of permission for performing platform actions within the account and on a service. For example, platform management roles that are assigned for catalog resources enable users to complete actions such as creating, deleting, editing, and viewing service instances. And, the platform management roles that are assigned for account management services enable users to complete actions such as inviting and removing users, working with resource groups, and viewing billing information. For more information about the account management services, see [Assigning access to account management services](/docs/account?topic=account-account-services).

Select all roles that apply when you create a policy. Each role allows separate actions to be completed and doesn't inherit the actions of the lesser roles.
{: tip}

The following table provides examples for some of the platform management actions that users can take within the context of catalog resources and resource groups. See the documentation for each catalog product to understand how the roles apply to users within the context of the service that is being used.


| Platform management role | One or all IAM-enabled services                                                      | Selected service in a resource group                | Resource group access |
|--------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------|-------------------------|
| Viewer role        | View instances and credentials                                   | View only specified instances in the resource group | View resource group     |
| Operator role      |  View instances and manage credentials                        |  Not applicable                                     | Not applicable          |
| Editor role        |  Create, delete, edit, and view instances. Manage credentials | Create, delete, edit, suspend, resume, view, and bind only specified instances in the resource group | View and edit name of resource group |
| Administrator role |  All management actions for services                                                 | All management actions for the specified instances in the resource group | View, edit, and manage access for the resource group |
{: row-headers}
{: caption="Example platform management roles and actions for services in an account" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to the selected role from the first column, and to the selected policy from the first row."}
{: #platformrolestable1}

For information about the specific actions users can take based on their assigned role on account management services, see [Assigning access to account management services](/docs/account?topic=account-account-services).
{: #acctmgmt}

Some services might map specific actions to the platform management roles that are related to the management of the service rather than to the access of the service. As an example, see the following table that details the {{site.data.keyword.containershort_notm}} service actions that are mapped to these roles.

| Platform management role | Actions                                                                                                    | Example actions for {{site.data.keyword.containershort_notm}} |
|--------------------------|------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| Viewer                   | Can view service instances, but can't modify them                                                          | - List clusters  \n - View details for a cluster|
| Editor                   | Perform all platform actions except for managing the account and assigning access policies                 |- Bind a service to a cluster  \n - Create a webhook|
| Operator                 | Perform platform actions required to configure and operate service instances, such as viewing a service's dashboard | - Add or remove worker nodes  \n - Restart or reload worker nodes  \n - Bind a service to a cluster |
| Administrator            | Perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users | - Remove a cluster  \n - Create a cluster  \n - Update user access policies  \n - All actions a viewer, editor, and operator can perform |
{: caption="Example platform management roles and actions for {{site.data.keyword.containershort_notm}} service" caption-side="top"}

### Service access roles
{: #service_access_roles}

Service access roles enable users to be assigned different levels of permission for calling the service's API and accessing the UI for the service. The following table provides example actions that can be taken depending on the assigned roles based on using the {{site.data.keyword.objectstorageshort}} service.

The actions that can be taken based on each assigned role vary based on the service that you selected for the policy. Not all services use these types of roles. See the documentation for the service for more details.
{: note}

| Service access role | Actions                                                                                       | Example actions for {{site.data.keyword.objectstorageshort}} service |
|---------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Reader              | Perform read-only actions within a service, such as viewing service-specific resources        | List and download objects                                            |
| Writer              | Permissions beyond the reader role, including creating and editing service-specific resources | Create and destroy buckets and objects                               |
| Manager             | Permissions beyond the writer role to complete privileged actions as defined by the service, plus create and edit service-specific resources | Manage all aspects of data storage, create, and destroy buckets and objects |
{: caption="Example service access user roles and actions" caption-side="top"}

### Custom access roles
{: #custom-access}

An account owner or a user assigned the Administrator role on the Role management service can create custom roles for a service on the IAM Roles page. Any number of actions that are available for a service for any platform or service role can be combined and added to a custom named role.

After the role is created, any user who can assign access for that service sees the new custom role as an option. For more information, see [Creating custom roles](/docs/account?topic=account-custom-roles).
