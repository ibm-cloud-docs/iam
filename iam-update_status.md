---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: user state, user status, change user status, update user status

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Updating a user's status
{: #status}

The status for a user depends on if the user accepted their invitation to join the account, if they're a VPN-only user, or if the administrator set the user as a disabled classic infrastructure user.
{: shortdesc}

If you have the following access, you can update the status of another user:

* An Identity and access management (IAM) policy with Editor or higher role on the User management service.
* You are an ancestor in the classic infrastructure hierarchy for the user and you have the Manage users classic infrastructure permission assigned

All account users are assigned a status that describes their user state. A user's status is displayed on the User details page.

| User State                      | Description                                                                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Active                          | The user accepted the invitation and has the assigned access to work within the account.                                                                      |
| Disabled classic infrastructure | The account owner or a user with sufficient permissions can set another user as disabled so that the user can no longer access classic infrastructure resources. The user can continue to log in to the console and access platform resources or support cases. |
| Invalid                   | A user's IAMid is deleted, and they can't access IAM-enabled resources. The user retains VPN access and can still use their classic infrastructure API key, but can't log in to the console. |
| Pending                         | A state in which a user is invited but hasn't accepted the invitation or joined the account by creating an {{site.data.keyword.cloud_notm}} account. |
| Processing                      | A rarely viewed state in which the user is added to an invite, the system creates the first instance of the user, but the invite hasn't been sent.    |
| Suspended                       |  The account owner or a user with sufficient permissions can set another user as suspended, which is a temporary alternative to removing a user. Access grants that are associated with the user through policies, access groups, or trusted profiles are not removed. A suspended user can log in to the {{site.data.keyword.cloud_notm}} console, but cannot perform any actions in the account where they are suspended. For CLI access, the user is restricted from both logging in and performing any actions.|
| VPN-only                        | A user that is created in the account, but is restricted to VPN access only for devices. This type of user doesn't have access to log in to the console.      |
{: caption="User status" caption-side="top"}

## Updating a user's status
{: #update_user_status}

To update a user's status, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Users**.
2. Select a user from the list.
3. From the User details page, select an option from the **User status** menu.
4. Click **Apply**.

### Status options
{: #status_options}

You can select from the following options to update a user's state:

Active
:   The user has full access to the {{site.data.keyword.cloud_notm}} console based on their assigned access policies and classic infrastructure permissions.

Disabled classic infrastructure
:   The user can no longer access classic infrastructure resources, but can continue to log in to the console and access platform resources.

Suspended
:   The user can't log in to the console, view the account in their account list, or use the CLI. All information and access policies that are associated with the user are saved.

VPN-only
:   The user can't log in to the console, but they can access the devices and VPN subnets that you assign for classic infrastructure by logging in directly to the appliance.

When you update a user from VPN-only status to Active status, the user must know the password to log in to the console. In most cases, the SoftLayer ID password is used, and it might need to be reset to be used. In rare cases where the user already has an IBMid, they must log in with the IBMid and password.
{: note}
