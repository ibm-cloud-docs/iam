---

copyright:

  years: 2023, 2026
lastupdated: "2026-03-20"

keywords: login session, end login session, monitor session, your login session, end all login sessions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring your login sessions
{: #monitor-your-session}

When you log in to the {{site.data.keyword.cloud}} console or {{site.data.keyword.cloud_notm}} command-line interface by using a user ID, a login session is created. You can review your active and expired login sessions on the [Login sessions page](/user/sessions){: external}. You can also end an individual session or all active sessions if a login-related credential, such as a refresh token or an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) cookie, is compromised.
{: shortdesc}

You can also review and end your own login sessions from the IAM Users page. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM)**, and select **Users**. Select your own user from the list, and click **View sessions** in the Details section to review your login sessions. 
{: tip}

## Reviewing your login sessions
{: #review-your-sessions}

To review your active and expired login sessions, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Profile** > **Login sessions**.
1. Review the list of your login sessions.

    By default, the page shows login sessions with all statuses, not active sessions only. If you want to change your view of the login sessions list and review only your active sessions, select **Active sessions** from the View dropdown menu.
    {: tip}

1. Click the **Table expand** icon ![Table expand icon](../icons/table-expand.svg "Table expand") on a session to view session details.

## Ending your login sessions
{: #end-your-sessions}

When you end an active login session, you are logged out and you're required to enter your credentials again. To end your active login session, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Profile** > **Login sessions**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the session that you want to end and select **End session**.
1. Click **End session** again to confirm that you want to end the session.

## Ending all active login sessions
{: #end-all-your-sessions}

You can also end all of your active sessions at once. Ending all of your active sessions logs you out of each session, so you can log in again by opening a session and entering your credentials. To end all of your login sessions at once, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to the **{{site.data.keyword.avatar}}** icon ![Avatar icon](../icons/i-avatar-icon.svg "Avatar") > **Profile** > **Login sessions**.
1. Click **End all sessions**.
1. Click **End all sessions** again to confirm that you want to end all of your sessions.
