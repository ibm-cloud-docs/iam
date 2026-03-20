---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: trusted profile, compute resource, granting access, tutorial, IAM trusted profile, trust relationship, establish trust, trust policy, trusted entity, assume access, apply access
subcollection: iam
content-type: tutorial
account-plan: lite
completion-time: 15m
services: containers

---

{{site.data.keyword.attribute-definition-list}}

# Managing access for apps in compute resources
{: #trustedprofile-compute-tutorial}
{: toc-content-type="tutorial"}
{: toc-services="containers"}
{: toc-completion-time="15m"}

This tutorial guides you through the steps to centrally manage fine-grained authorization for all applications that are running in a compute resource without creating service IDs or managing the API key lifecycle for applications. By completing this tutorial, you learn how to create a trusted profile, establish trust with compute resources based on specific attributes, and define a policy to assign access to resources.
{: shortdesc}

By using trusted profiles, you can establish a flexible, secure way for apps that are running on a compute resource to access other {{site.data.keyword.cloud}} resources. All compute resource instances that share certain attributes, such as name, namespace, tags, or location, are mapped to a common profile and can share access to {{site.data.keyword.cloud_notm}} resources. This common identity makes it possible to give the applications within various compute resources access to an external resource one time, rather than cluster-by-cluster.

You must enable the **Service Account Token Volume Projection** on the Kubernetes cluster to apply the trusted profile identity. For more information, see [Authorizing pods in your cluster to IBM Cloud services with IAM trusted profiles](/docs/containers?topic=containers-pod-iam-identity&interface=ui)
{: note}

Let's say that you are the lead developer on a project for your team that is planning to run a new chatbot app on an {{site.data.keyword.containerfull}} cluster. You want the app to have access to IAM-enabled services but without storing credentials in the code. Your manager has given you an administrator access in the account to create trusted profiles and give your runtime environments access to the resources you need to build the chatbot app.

## Before you begin
{: #trusted-profile-compute-prereqs}

* This tutorial might incur costs. Use the [Cost Estimator](/estimator) to generate a cost estimate based on your projected usage.
* Make sure you have the following access:
   * Administrator role in the account to create a trusted profile
   * Administrator role on the specific resources to which you are assigning access
* Create a cluster that runs {{site.data.keyword.containerlong_notm}} Version 1.21 or later. For information about creating a cluster, see [Getting started with IBM Cloud Kubernetes Service](/docs/containers?topic=containers-getting-started).

## Create a trusted profile
{: #trusted-profile-compute-create}
{: step}

First, create your trusted profile:

1. Go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select **Trusted profiles**.
2. Click **Create profile**.
3. Name the profile `Chatbot Project`.
4. In the description, list the level of access you want to assign to the profile. This helps you quickly identify different profiles from the list of trusted profiles. In this case:
   1. Writer
   2. Manager
5. Click **Continue**.

Make sure that your profile name is short and human readable. For compute resources, the name of the profile is required to get the compute resource token, so a simple name is easier for developers to use in the program.
{: note}

## Establish trust with the Kubernetes cluster
{: #trusted-profile-compute-trust}
{: step}

Now that you created your trusted profile, you want to establish trust with the Kubernetes cluster you created for the project:

1. For trust entity type, select **Compute resources**.
2. For compute service, select **Kubernetes** from the list.
3. Select **Specific resources** to establish trust with one or more existing compute resource instances.
4. Click **Add another resource**.
5. Select the cluster that you created for this tutorial.
6. Enter the values for the `namespace` and `service account` fields.

   The Kubernetes namespace and service account names that you enter do not have to exist already. Any future namespaces or service accounts with these names can establish trust. To list existing namespaces, log in to your cluster and run `kubectl get ns`. To list existing service accounts, log in to your cluster and run `kubectl get sa -n <namespace>`. You can also enter `default` for both.
   {: tip}

7. Click **Continue**.

## Assign access to other {{site.data.keyword.cloud_notm}} services
{: #trusted-profile-compute-access}
{: step}

Now, you can create an access policy to give your compute resource instance access to other IBM Cloud services you need for your team's chatbot project.

1. Select **Access policy**.
2. Select **Watson Assistant** from the list of services. Make sure you have access on the service you want to give access to in this profile.Click **Next**.
3. Scope the access to **Specific resources** based on selected attributes.
4. Select **Service Instance** and input the service instance name to give permission to a specific instance. Click **Next**.
5. Select Writer and Manager roles to define the scope of access, and click **Review**.
6. Click **Add** to add your policy configuration to your policy summary.
7. Click **Assign**.

## Next steps
{: #iam-compute-next}

To learn more about establishing trust with a Kubernetes cluster, see [Using Trusted Profiles in your Kubernetes and OpenShift Clusters](https://www.ibm.com/products){: external}. To learn how to use trusted profiles with VPC virtual server instances, see [Introducing Trusted Profiles for VPC Virtual Server Instances](https://www.ibm.com/think){: external}.

Now that you learned the basics of how to create a trusted profile, you can continue to establish trust with additional compute resources. For more information, see [Updating trusted profiles](/docs/account?topic=account-trusted-profile-update).

You can also use {{site.data.keyword.cloudaccesstrailshort}} to monitor which federated users and compute resources apply a trusted profile. For more information, see [Monitoring login sessions for trusted profiles](/docs/account?topic=account-trusted-profile-monitor).
