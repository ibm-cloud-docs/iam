---

copyright:

  years: 2026, 2026
lastupdated: "2026-06-30"

keywords: trusted profile, Power Virtual Server, PowerVS, SAP workloads, granting access, tutorial, IAM trusted profile, trust relationship, establish trust, trust policy, trusted entity, assume access, apply access
subcollection: iam
content-type: tutorial
account-plan: lite
completion-time: 20m

---

{{site.data.keyword.attribute-definition-list}}

# Managing access for SAP workloads in {{site.data.keyword.powerSys_notm}}
{: #trustedprofile-powervs-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="20m"}

This tutorial guides you through the steps to centrally manage fine-grained authorization for SAP applications running on {{site.data.keyword.powerSys_notm}} without creating service IDs or managing the API key lifecycle. By completing this tutorial, you learn how to create a trusted profile, establish trust with {{site.data.keyword.powerSys_notm}} instances based on specific attributes, and define a policy to assign access to {{site.data.keyword.cos_full_notm}} for secure backups.
{: shortdesc}

By using trusted profiles, you can establish a flexible, secure way for SAP workloads running on {{site.data.keyword.powerSys_notm}} to access other {{site.data.keyword.cloud}} resources. All {{site.data.keyword.powerSys_notm}} instances that share certain attributes, such as workspace, instance name, or location, are mapped to a common profile and can share access to {{site.data.keyword.cloud_notm}} resources.

Let's say you are managing SAP workloads on {{site.data.keyword.powerSys_notm}} and need to enable automated backups to {{site.data.keyword.cos_short}}. You want your SAP systems to have access to Cloud Object Storage without storing credentials in the application code or configuration files. Your manager has given you administrator access in the account to create trusted profiles and assign the necessary permissions.

## Before you begin
{: #trusted-profile-powervs-prereqs}

* This tutorial might incur costs. Use the [Cost Estimator](/estimator){: external} to generate a cost estimate based on your projected usage.
* Make sure you have the following access:
   * Administrator role in the account to create a trusted profile
   * Administrator role on the specific resources to which you are assigning access
* Create a {{site.data.keyword.powerSys_notm}} workspace and instance. For information about creating {{site.data.keyword.powerSys_notm}} resources, see [Getting started with {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-getting-started).
* Create a {{site.data.keyword.cos_short}} instance for storing backups. For more information, see [Getting started with {{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

## Create a trusted profile
{: #trusted-profile-powervs-create}
{: step}

First, create your trusted profile:

1. Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select **Trusted profiles**.
2. Click **Create profile**.
3. Name the profile `SAP Backup Profile`.
4. In the description, briefly describe the profile's purpose and the level of access it grants. This helps you quickly identify different profiles from the list of trusted profiles.
   - For example: `Writer access to Cloud Object Storage for SAP backup operations`.
5. Click **Continue**.

Make sure that your profile name is short and human readable. For compute resources, the name of the profile is required to get the compute resource token, so a simple name is easier for developers to use in applications.
{: note}

## Establish trust with {{site.data.keyword.powerSys_notm}}
{: #trusted-profile-powervs-trust}
{: step}

Now that you created your trusted profile, you want to establish trust with your {{site.data.keyword.powerSys_notm}} instances:

1. For trust entity type, select **Compute resources**.
2. For compute service, select **{{site.data.keyword.powerSys_notm}}** from the list.
3. Select **All service resources** to establish trust with {{site.data.keyword.powerSys_notm}} instances based on conditions.
4. Click **Add a condition** to define which {{site.data.keyword.powerSys_notm}} instances can use this profile.
5. Add conditions based on your requirements. For example:
   * Workspace CRN (`workspaces.crn`)
   * Subnet CRN (`subnets.crn`)
   * Instance CRN (`iaas.crn`)
   * Instance name (`iaas.name`)
   * Account ID (`iaas.account_id`)
   * Zone (`iaas.zone`)
   * Region (`iaas.region`)
   * Resource group ID (`iaas.resource_group_id`)

   Any {{site.data.keyword.powerSys_notm}} instances that meet all the conditions can establish trust with this profile.
   {: tip}

6. Click **Continue**.

## Assign access to {{site.data.keyword.cos_short}}
{: #trusted-profile-powervs-access}
{: step}

Now, you can create an access policy to give your {{site.data.keyword.powerSys_notm}} instances access to {{site.data.keyword.cos_short}} for backup operations.

1. Select **Access policy**.
2. Select **Cloud Object Storage** from the list of services. Make sure you have access on the service you want to give access to in this profile. Click **Next**.
3. Scope the access to **Specific resources** based on selected attributes.
4. Select **Service Instance** and input the service instance name to give permission to a specific Cloud Object Storage instance. Click **Next**.
5. Select Writer role to define the scope of access for backup operations, and click **Review**.
6. Click **Add** to add your policy configuration to your policy summary.
7. Click **Assign**.

## Next steps
{: #iam-powervs-next}

Now that you learned the basics of how to create a trusted profile for {{site.data.keyword.powerSys_notm}}, you can:

* Configure your SAP applications to use the trusted profile for accessing Cloud Object Storage
* Establish trust with additional {{site.data.keyword.powerSys_notm}} instances
* Monitor which {{site.data.keyword.powerSys_notm}} instances apply the trusted profile using {{site.data.keyword.cloudaccesstrailshort}}

For more information, see [Updating trusted profiles](/docs/iam?topic=iam-trusted-profile-update) and [Monitoring login sessions for trusted profiles](/docs/iam?topic=iam-trusted-profile-monitor).
