---

copyright:

  years: 2023, 2026
lastupdated: "2026-05-06"

keywords: context-based restrictions, protecting catalog resources, security, catalog management, security, workloads

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Protecting catalogs with context-based restrictions
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to catalogs can be controlled with context-based restrictions and identity and access management (IAM) policies.
{: shortdesc}

These restrictions work with traditional IAM policies, which are based on identity, to provide another layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. See [What are context-based restrictions?](/docs/iam?topic=iam-context-restrictions-whatis) for more information.

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated come from the context-based restrictions service, not Catalog Management. For more information, see [Monitoring context-based restrictions](/docs/iam?topic=iam-cbr-monitor).

## Before you begin
{: #before-cm-cbr}

Review the following access requirements:

- A user must have the Administrator role on the Catalog Management service to create, update, or delete rules.
- A user must also have either the Editor or Administrator role on the Context-based restrictions service to create, update, or delete network zones.
- A user with the Viewer role on the Context-based restrictions service can add only network zones to a rule.

To get started protecting your catalogs with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/iam?topic=iam-context-restrictions-tutorial).

## How catalogs integrate with context-based restrictions
{: #cbr-overview-cm}

### Protecting specific APIs
{: #cm-cbr-apis}

You can create context-based restrictions to protect the following APIs for the Catalog Management Service.

Service APIs
:   Target Service APIs to protect actions like sharing private catalogs and managing catalog settings.

Platform APIs
:   Target Platform APIs to protect create, update, and delete actions on your private catalogs. When a context-based restriction is protecting the Catalog Management Platform APIs, users must satisfy the rule to view the private catalogs that you specify.

### Protecting specific resources
{: #cm-cbr-attributes}

You can protect specific resources by scoping your rule to the available attributes for Catalog Management.

Catalog
:   Scope your rule to protect a specific private catalog. Users can view the catalog that you protect only if they satisfy your context rule.

## Limitations
{: #cbr-limitations-cm}

Context-based restrictions protect only the actions associated with the [Catalog Management API](/apidocs/resource-catalog/private-catalog). For more information, see [IAM roles and actions](/docs/iam?topic=iam-iam-service-roles-actions&interface=ui#globalcatalog-collection-roles). Actions that are associated with the following platform APIs are not protected by context-based restrictions. Reference the API docs for the specific action IDs.

- [Resource Instance APIs](/apidocs/resource-controller/resource-controller#list-resource-instances)
- [Resource Keys APIs](/apidocs/resource-controller/resource-controller#list-resource-keys)
- [IAM Policy APIs](/apidocs/iam-policy-management#list-policies)
- [Global Search APIs](/apidocs/search)
- Global Tagging [Attach](/apidocs/tagging#attach-tag) and [Detach](/apidocs/tagging#detach-tag) APIs
- [Context-based Restriction Rule APIs](/apidocs/context-based-restrictions#create-rule)
- [Secrets Manager APIs](/apidocs/secrets-manager)


## Creating network zones
{: #network-zone-cm}

A network zone represents an allowlist of IP addresses where an access request is created. It defines a set of one or more network locations that are specified by the following attributes:

* IP addresses, which include individual addresses, ranges, or subnets.
* VPCs
* Service references, which allow access from other {{site.data.keyword.cloud_notm}} services.

Make sure to add Catalog Management to network zones for rules that target other {{site.data.keyword.cloud_notm}} resources, or some operations in your workflow might fail.
{: important}

### Service references
{: #service-ref-cm}

Add the Catalog Management Service (`globalcatalog-collection`) to your network zones for rules created against the following services. This way, the two services can continue to communicate.

Secrets Manager
:   If you have a rule that protects Secrets Manager and you’re [onboarding a product with Secrets Manager](/docs/account?topic=account-create-private-catalog&interface=ui#add-public-repo-ui), add your IP address and the Catalog Management service to a network zone as a service reference.

Schematics
:   If you're using a [target account](/docs/iam?topic=iam-create-trusted-profile&interface=ui#create-profile-services) to validate a product and you have a rule protecting Schematics in the target account, add the Catalog Management service to a network zone as a service reference.

Similarly, if you have a rule that targets the Catalog Management Service, add the Schematics service as a service reference in the network zone.
{: important}

IAM Identity
:   If you have a rule scoped to protect the entire IAM Identity service or scoped to the [trusted profile that you use for validation](/docs/iam?topic=iam-create-trusted-profile&interface=ui#create-profile-services), add the Catalog Management service to a network zone as a service reference so that the validation flow still works.

Make sure to add that network zone to your context-based restriction rule. This way, the two services can continue to communicate.
{: tip}

### Example by using the console
{: #service-ref-cm-ex}
{: ui}

By creating network zones, you establish a list of allowed locations where an access request originates. Add the Catalog Management service to that allowlist as a service reference. After you create a network zone, you can add it to a rule.

To create a network zone, complete the following steps:
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Network zones**.
1. Click **Create**.

    Instead of creating a zone by using UI inputs, you can use the JSON code form to directly enter JSON to create a zone by clicking **Enter as JSON code**.
    {: note}

1. Enter a unique name and a description. For example, `Catalog zone` and `Allow catalogs to interact with other services`.
1. Reference a service. Select the service type "IAM services" and then select the Catalog Management service. Click **Add** to associate the service's IP addresses with your network zone.
1. Click **Next** to review your network zone.
1. Click **Create**.


### Example by using the CLI
{: #service-ref-cm-ex-cli}
{: cli}

By creating network zones, you establish a list of allowed locations where an access request originates. Add the Catalog Management service to that allowlist as a service reference. After you create a network zone, you can add it to a rule.

1. Install the [Context-based restrictions CLI plug-in](/docs/iam?topic=iam-cbr-plugin) by running the following command:

  ```sh
    ibmcloud plugin install cbr
    ```
  {: pre}

1. To create a network zone, use the [cbr zone-create](/docs/iam?topic=iam-cbr-plugin#cbr-cli-zone-create-command) command.


   The following example creates a network zone with a service reference. For more information, see [Service references](/docs/iam?topic=iam-context-restrictions-whatis&interface=cli#service-attribute).

  ```sh
    ibmcloud cbr zone-create --name CatalogZone --description "Allow catalogs to interact with other services" --service-ref service_name=globalcatalog-collection
    ```
    {: pre}

    To find a list of available service references, run the [ibmcloud cbr service-ref-targets](/docs/iam?topic=iam-cbr-plugin#cbr-cli-service-ref-targets-command) command.
    {: tip}


### Example by using the API
{: #service-ref-cm-ex-api}
{: api}

By creating network zones, you establish a list of allowed locations where an access request originates. Add the Catalog Management service to that allowlist as a service reference. After you create a network zone, you can add it to a rule.

To create a network zone that includes the Catalog Management service, call the [Context-based restrictions API](/apidocs/context-based-restrictions#create-zone) as shown in the following example:

```sh
{
  "name": "Catalog zone",
  "description": "Allow catalogs to interact with other services",
  "addresses": [
    {
      "type": "serviceRef",
      "ref": {
        "service_name": "globalcatalog-collection"
      }
    }
  ]
}
```
{: codeblock}
{: curl}

```java
AddressIPAddress ipAddressModel = new AddressIPAddress.Builder()
ServiceRefValue serviceRefValueModel = new ServiceRefValue.Builder()
  .accountId(accountID)
  .serviceName("globalcatalog-collection")
  .build();
AddressServiceRef serviceRefAddressModel = new AddressServiceRef.Builder()
  .type("serviceRef")
  .ref(serviceRefValueModel)
  .build();
CreateZoneOptions createZoneOptions = new CreateZoneOptions.Builder()
  .name("Catalog zone")
  .accountId(accountID)
  .description("Allow catalogs to interact with other services")
  .addresses(java.util.Arrays.asList(ipAddressModel, ipRangeAddressModel, subnetAddressModel, vpcAddressModel, serviceRefAddressModel))
  .excluded(java.util.Arrays.asList(excludedIPAddressModel))
  .build();

Response<Zone> response = contextBasedRestrictionsService.createZone(createZoneOptions).execute();
Zone zone = response.getResult();

System.out.println(zone);
```
{: codeblock}
{: java}

```javascript
// Request models needed by this operation.

// AddressServiceRef
const serviceRefAddressModel = {
  type: 'serviceRef',
  ref: {
    account_id: accountId,
    service_name: 'globalcatalog-collection',
  },
};

const params = {
  name: 'Catalog zone',
  accountId,
  addresses: [ipAddressModel, ipRangeAddressModel, subnetAddressModel, vpcAddressModel, serviceRefAddressModel],
  excluded: [excludedIPAddressModel],
  description: 'Allow catalogs to interact with other services',
};

try {
  const res = await contextBasedRestrictionsService.createZone(params);
  zoneId = res.result.id;
  zoneRev = res.headers.etag;
  console.log(JSON.stringify(res.result, null, 2));
} catch (err) {
  console.warn(err);
}
```
{: codeblock}
{: javascript}

```python
service_ref_address_model = {
  'type': 'serviceRef',
  'ref': {
    'account_id': account_id,
    'service_name': 'globalcatalog-collection',
  }
}

zone = context_based_restrictions_service.create_zone(
  name='catalog zone',
  account_id=account_id,
  addresses=[service_ref_address_model],
  description='allow catalogs to interact with other services',
).get_result()

print(json.dumps(zone, indent=2))
```
{: codeblock}
{: python}

```go
serviceRefAddressModel := &contextbasedrestrictionsv1.AddressServiceRef{
  Type: core.StringPtr("serviceRef"),
  Ref: &contextbasedrestrictionsv1.ServiceRefValue{
    AccountID:   core.StringPtr(accountID),
    ServiceName: core.StringPtr("globalcatalog-collection"),
  },

createZoneOptions := contextBasedRestrictionsService.NewCreateZoneOptions()
createZoneOptions.SetName("catalog zone")
createZoneOptions.SetAccountID(accountID)
createZoneOptions.SetDescription("allow catalogs to interact with other services")
createZoneOptions.SetAddresses([]contextbasedrestrictionsv1.AddressIntf{serviceRefAddressModel})

zone, response, err := contextBasedRestrictionsService.CreateZone(createZoneOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(zone, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}

To find a list of available service references, call the [ListAvailableServicerefTargets](/apidocs/context-based-restrictions?code=go#list-available-serviceref-targets) method.
{: tip}

## Creating network zones by using Terraform
{: #network-zones-create-terra}
{: terraform}

By creating network zones, you establish a list of allowed locations where an access request originates. Add the Catalog Management service to that allowlist as a service reference. After you create a network zone, you can add it to a rule.

To create a network zone, use the Terraform resource [cbr_zone](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cbr_zone).

1. To install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform, follow the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a network zone by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

    The following example creates a network zone that allows a single IP address and explicitly excludes a single IP address.

    ```terraform
    resource "ibm_cbr_zone" "cbr_zone" {
      account_id = "12ab34cd56ef78ab90cd12ef34ab56cd"
      addresses {
            type = "serviceRef"
            value = "globalcatalog-collection"
      }
      description = "allow catalogs to interact with other services"
      name = "catalog zone"
    }
    ```
    {: codeblock}
