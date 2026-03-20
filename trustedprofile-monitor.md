---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: trusted profile, generating IAM token, compute resource, kubernetes cluster, virtual server

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring login sessions for trusted profiles
{: #trusted-profile-monitor}

Trusted profiles are used to automatically grant federated users access to your account, and you can use {{site.data.keyword.logs_full_notm}} to monitor which federated users and compute resources apply a trusted profile.
{: shortdesc}

For more information, see [Activity tracking events for IAM](/docs/account?topic=account-at_events_iam).

You can also monitor active user login sessions. For more information, see [Monitoring your login sessions](/docs/account?topic=account-monitor-your-session).

## Before you begin
{: #before-monitor}

You must create an instance of the {{site.data.keyword.logs_full_notm}} service in the `Frankfurt (eu-de)` region to monitor events for IAM trusted profiles. For more information, see [Creating an IBM Cloud Logs service instance](/docs/cloud-logs?topic=cloud-logs-getting-started#gs-creating-instance).

## Reviewing login sessions by using {{site.data.keyword.logs_full_notm}}
{: #trusted-profile-review-at}

Complete the following steps to review login sessions by using {{site.data.keyword.logs_full_notm}}:

1. In the {{site.data.keyword.cloud_notm}} console, go to the **Navigation Menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") > **Observability** > **Logging** > **Instances** > **Cloud Logs**.
1. Click **Open dashboard** on the dashboard that you use to monitor trusted profiles.
1. Go to **Subsystems** and select **iam-identity** to filter the results and view only IAM Identity login events.
1. Use the search field to view trusted profiles login events for users or to view trusted profiles login events for compute resources.
   1. For users, search `action:iam-identity.user-authcode OR action:iam-identity.user-identitycookie.login`.
      * `action:iam-identity.user-authcode` indicates a login that is initiated by the user.
      * `action:iam-identity.user-identitycookie.login` indicates an authentication that is based on a browser cookie.
   1. For compute resources, search `action:iam-identity.computeresource-token.login`.
1. Select an event to view the fields that have identifying information:
   * The `Initiator.authnId` and `Initiator.authnName` attributes contain the details for the authenticated user that applies a profile.
   * The `Initiator.id` and `Initiatior.name` attributes contain the details of the profile that is applied.


### Examples
{: #trusted-profile-monitor-example}

A compute resource that's applying trusted profile `compute-profile-1` has the following identifying attributes:

| Attribute    | Value      |
|---------------|------------|
| action        | `iam-identity.computeresource-token.login` |
| initiator.name | `compute-profile-1` |
| initiator.id  | `IBMid08348934` |
| initiator.typeURI | `service/security/account/profile` |
| initiator.credential.type | `profile` |
| initiator.authnId | `crn-crn:v1:bluemix:public:containers-kubernetes:satloc_wdc_c8gfp9ow)1il4mg:a/a319e5b2c84429a9a2ece7a7c9a8807:c8jrclfw0` |
| initiator.authnName | `sat-kp-c8gfp9ow0gavb01il4mg:ibm-kp:default:key-management-crypto-7797c45798-mlbck` |
| logsourceCRN | `crn:v1:bluemix:public:cloud-object-storage:global:a/59bcbfa6ea2f006b4ed7094c1a08dcdd:1a0ec336-f391-4091-a6fb-5e084a4c56f4::` |
{: caption="Sample trusted profile attributes and values from {{site.data.keyword.atracker_full_notm}}" caption-side="top"}

A federated user that's applying trusted profile `fed-user-profile-1` has the following identifying attributes:

| Attribute    | Value      |
|---------------|------------|
| action        | `iam-identity.user-authcode` |
| initiator.name | `fed-user-profile-1` |
| initiator.id  | `IBMid90101838` |
| initiator.typeURI | `service/security/account/profile` |
| initiator.credential.type | `profile` |
| initiator.authnId | `IBMid11118967` |
| initiator.authnName | `addison.martin@ibm.com` |
{: caption="Sample trusted profile attributes and values from {{site.data.keyword.atracker_full_notm}}" caption-side="top"}


