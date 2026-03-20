---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-20"

keywords: create network access, network access rule, network zone

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Creating context-based restrictions
{: #context-restrictions-create}

Context-based restrictions allow you to manage user and service access to specific cloud resources. You can define restrictions to the resources based on contexts, such as network zones and endpoint types. For more information, see [What are context-based restrictions](/docs/iam?topic=iam-context-restrictions-whatis&interface=ui).
{: shortdesc}

User and account-level IP address restrictions can also affect users' ability to access resources. You can view account-level IP address restrictions on the [Settings](/iam/settings) page. To view individual user settings, go to the [Users](/iam/users) page and view each user's IP address restrictions in the details tab.
{: note}

## Before you begin
{: #context-prereq}

* To complete rule actions, you must be assigned an Identity and Access Management (IAM) policy on the target service.
* To complete network zone actions, you must be assigned an IAM policy on the context-based restrictions service.

For more information, see [Context-based restrictions roles and actions](/docs/iam?topic=iam-context-restrictions-whatis#cbr-access-reqs-cbr-restrict).

## Creating network zones
{: #network-zones-create}
{: ui}

By creating network zones, you establish a list of allowed locations where an access request originates. A set of one or more network locations can be specified by IP addresses such as individual addresses, ranges or subnets, and VPC IDs. After you create a network zone, you can add it to a rule.

To create a network zone, complete the following steps.
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Network zones**.
1. Click **Create**.

    Instead of creating a zone by using UI inputs, you can use the JSON code form to directly enter JSON to create a zone by clicking **Enter as JSON code**.
    {: note}

1. Enter a unique name and a description.
1. Enter the allowed IP addresses where an access request can originate. Include IP address exceptions in the deny list, if necessary.
1. Enter the allowed VPCs.

    If you want to allow access from the VPC to public endpoints in your rule, include any public gateway IP addresses in the zone definition along with the VPC.
    {: important}

1. Reference a service. Select the service type and then select a service. Click **Add** to associate the service's IP addresses with your network zone.

    If you're not sure what the service type is, view the table [Services integrated with context-based restrictions](/docs/iam?topic=iam-context-restrictions-whatis#cbr-adopters).
    {: tip}

1. Click **Next** to review your network zone.
1. Click **Create**.

You can continue by creating more network zones, or by creating rules.


## Creating network zones by using the CLI
{: #network-zones-create-cli}
{: cli}

By creating network zones, you establish a list of allowed locations where an access request originates. A set of one or more network locations can be specified by IP addresses such as individual addresses, ranges or subnets, and VPC IDs. After you create a network zone, you can add it to a rule.

1. Install the [Context-based restrictions CLI plug-in](/docs/iam?topic=iam-cbr-plugin) by running the following command:

   ```sh
   ibmcloud plugin install cbr
   ```
   {: pre}

1. To create a network zone, use the [cbr zone-create](/docs/iam?topic=iam-cbr-plugin#cbr-cli-zone-create-command) command.

   The following example creates a network zone with a list of allowed network locations.

   ```sh
   ibmcloud cbr zone-create --name example-zone --description "Example zone description" --addresses 192.0.2.1,192.2.3.5-192.2.3.10
   ```
   {: pre}

   The following example creates a network zone with a service reference. For more information, see [Service references](/docs/iam?topic=iam-context-restrictions-whatis&interface=cli#service-attribute).

    ```sh
    ibmcloud cbr zone-create --name example-zone-1 --description "Kube zone" --service-ref service_name=containers-kubernetes
    ```
    {: pre}

    To find a list of available service references, run the [ibmcloud cbr service-ref-targets](/docs/iam?topic=iam-cbr-plugin#cbr-cli-service-ref-targets-command) command.
    {: tip}


## Creating network zones by using the API
{: #network-zones-create-api}
{: api}

By creating network zones, you establish a list of allowed locations where an access request originates. A set of one or more network locations can be specified by IP addresses such as individual addresses, ranges or subnets, VPC IDs, and service references. After you create a network zone, you can add it to a rule.

To create a network zone, call the [Context-based restrictions API](/apidocs/context-based-restrictions#create-zone) as shown in the following example:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "name": "an example of zone", "description": "this is an example of zone", "account_id": "12ab34cd56ef78ab90cd12ef34ab56cd", "addresses": [ { "type": "ipAddress", "value": "169.23.56.234" }, { "type": "ipRange", "value": "169.23.22.0-169.23.22.255" }, { "type": "subnet", "value": "192.0.2.0/24" }, { "type": "vpc", "value": "crn:v1:bluemix:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r134-d98a1702-b39a-449a-86d4-ef8dbacf281e" }, { "type": "serviceRef", "ref": { "account_id": "12ab34cd56ef78ab90cd12ef34ab56cd", "service_name": "cloud-object-storage" } } ], "excluded": [ { "type": "ipAddress", "value": "169.23.22.127" } ] }' "{base_url}/v1/zones"
```
{: codeblock}
{: curl}

```java
AddressIPAddress ipAddressModel = new AddressIPAddress.Builder()
  .type("ipAddress")
  .value("169.23.56.234")
  .build();
AddressIPAddressRange ipRangeAddressModel = new AddressIPAddressRange.Builder()
  .type("ipRange")
  .value("169.23.22.0-169.23.22.255")
  .build();
AddressSubnet subnetAddressModel = new AddressSubnet.Builder()
  .type("subnet")
  .value("192.0.2.0/24")
  .build();
AddressVPC vpcAddressModel = new AddressVPC.Builder()
  .type("vpc")
  .value(vpcCRN)
  .build();
ServiceRefValue serviceRefValueModel = new ServiceRefValue.Builder()
  .accountId(accountID)
  .serviceName("cloud-object-storage")
  .build();
AddressServiceRef serviceRefAddressModel = new AddressServiceRef.Builder()
  .type("serviceRef")
  .ref(serviceRefValueModel)
  .build();
AddressIPAddress excludedIPAddressModel = new AddressIPAddress.Builder()
  .type("ipAddress")
  .value("169.23.22.127")
  .build();
CreateZoneOptions createZoneOptions = new CreateZoneOptions.Builder()
  .name("an example of zone")
  .accountId(accountID)
  .description("this is an example of zone")
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

// AddressIPAddress
const ipAddressModel = {
  type: 'ipAddress',
  value: '169.23.56.234',
};
// AddressIPAddressRange
const ipRangeAddressModel = {
  type: 'ipRange',
  value: '169.23.22.0-169.23.22.255',
};
// AddressSubnet
const subnetAddressModel = {
  type: 'subnet',
  value: '192.0.2.0/24',
};
// AddressVPC
const vpcAddressModel = {
  type: 'vpc',
  value: vpcCRN,
};
// AddressServiceRef
const serviceRefAddressModel = {
  type: 'serviceRef',
  ref: {
    account_id: accountId,
    service_name: 'cloud-object-storage',
  },
};
// AddressIPAddress
const excludedIPAddressModel = {
  type: 'ipAddress',
  value: '169.23.22.127',
};

const params = {
  name: 'an example of zone',
  accountId,
  addresses: [ipAddressModel, ipRangeAddressModel, subnetAddressModel, vpcAddressModel, serviceRefAddressModel],
  excluded: [excludedIPAddressModel],
  description: 'this is an example of zone',
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
ip_address_model = {
  'type': 'ipAddress',
  'value': '169.23.56.234',
}
ip_range_address_model = {
  'type': 'ipRange',
  'value': '169.23.22.0-169.23.22.255',
}
subnet_address_model = {
  'type': 'subnet',
  'value': '192.0.2.0/24',
}
vpc_address_model = {
  'type': 'vpc',
  'value': vpc_crn,
}
service_ref_address_model = {
  'type': 'serviceRef',
  'ref': {
    'account_id': account_id,
    'service_name': 'cloud-object-storage',
  }
}
excluded_ip_address_model = {
  'type': 'ipAddress',
  'value': '169.23.22.127',
}

zone = context_based_restrictions_service.create_zone(
  name='an example of zone',
  account_id=account_id,
  addresses=[ip_address_model, ip_range_address_model, subnet_address_model, vpc_address_model, service_ref_address_model],
  excluded=[excluded_ip_address_model],
  description='this is an example of zone',
).get_result()

print(json.dumps(zone, indent=2))
```
{: codeblock}
{: python}

```go
ipAddressModel := &contextbasedrestrictionsv1.AddressIPAddress{
  Type:  core.StringPtr("ipAddress"),
  Value: core.StringPtr("169.23.56.234"),
}
ipRangeAddressModel := &contextbasedrestrictionsv1.AddressIPAddressRange{
  Type:  core.StringPtr("ipRange"),
  Value: core.StringPtr("169.23.22.0-169.23.22.255"),
}
subnetAddressModel := &contextbasedrestrictionsv1.AddressSubnet{
  Type:  core.StringPtr("subnet"),
  Value: core.StringPtr("192.0.2.0/24"),
}
vpcAddressModel := &contextbasedrestrictionsv1.AddressVPC{
  Type:  core.StringPtr("vpc"),
  Value: core.StringPtr(vpcCRN),
}
serviceRefAddressModel := &contextbasedrestrictionsv1.AddressServiceRef{
  Type: core.StringPtr("serviceRef"),
  Ref: &contextbasedrestrictionsv1.ServiceRefValue{
    AccountID:   core.StringPtr(accountID),
    ServiceName: core.StringPtr("cloud-object-storage"),
  },
}
excludedIPAddressModel := &contextbasedrestrictionsv1.AddressIPAddress{
  Type:  core.StringPtr("ipAddress"),
  Value: core.StringPtr("169.23.22.127"),
}

createZoneOptions := contextBasedRestrictionsService.NewCreateZoneOptions()
createZoneOptions.SetName("an example of zone")
createZoneOptions.SetAccountID(accountID)
createZoneOptions.SetDescription("this is an example of zone")
createZoneOptions.SetAddresses([]contextbasedrestrictionsv1.AddressIntf{ipAddressModel, ipRangeAddressModel, subnetAddressModel, vpcAddressModel, serviceRefAddressModel})
createZoneOptions.SetExcluded([]contextbasedrestrictionsv1.AddressIntf{excludedIPAddressModel})

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
{: #network-zones-create-terraform}
{: terraform}

By creating network zones, you establish a list of allowed locations where an access request originates. A set of one or more network locations can be specified by IP addresses such as individual addresses, ranges or subnets, VPC IDs, and service references. After you create a network zone, you can add it to a rule.

To create a network zone, use the Terraform resource [cbr_zone](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cbr_zone).

1. To install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform, follow the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a network zone by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

    The following example creates a network zone that allows a single IP address and explicitly excludes a signle IP address.

    ```terraform
    resource "ibm_cbr_zone" "cbr_zone" {
      account_id = "12ab34cd56ef78ab90cd12ef34ab56cd"
      addresses {
            type = "ipAddress"
            value = "169.23.56.234"
      }
      description = "this is an example of zone"
      excluded {
            type = "ipAddress"
            value = "202.38.89.897"
      }
      name = "an example of zone"
    }
    ```
    {: codeblock}

## Creating rules
{: #context-restrictions-create-rules}
{: ui}

Define restrictions to your cloud resources by creating rules.

To create a rule, complete the following steps.
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Rules**.
1. Click **Create**.
1. Select the service that you want to target in your rule. Then, click **Next**.
    
    When you create context-based restriction for the IAM Access Groups service, users who don't satisfy the rule can't view any groups in the account, including the public access group.
    {: note}

1. (Optional) Select the scope of APIs whose operations are restricted by your rule. For more information, see [Defining the scope of a rule](/docs/iam?topic=iam-context-restrictions-whatis&interface=ui#rule-scope).

    Not all services support the ability to scope a rule by API.
    {: note}

1. Scope the restriction to **All resources** or **Specific resources** based on selected attributes.
1. Click **Review** > **Continue**.
1. Add one or more contexts. Select endpoint types and network zones, and click **Add**.
    * By default, access is allowed from all service-supported endpoint types when the toggle is set to No. Set the toggle to Yes to allow only specific endpoint types.

    If you want to allow access from a VPC to public endpoints in your rule, include any public gateway IP addresses in the zone definition along with the VPC.
    {: important}

    * You can add existing network zones to your rule or create new zones to add to your rule. For more information, see [Creating network zones](/docs/iam?topic=iam-context-restrictions-create&interface=ui#network-zones-create).
1. Click **Continue**.
1. Provide a unique description.
1. Select how you want to enforce the rule. You can decide how you want to enforce a rule upon creation and update the rule enforcement at any time.
    * **Enable**: Enforce the rule. Denied access attempts are reported in {{site.data.keyword.atracker_short}}.
    * **Disable**: Don't enforce the rule. Restrictions don't apply to your account resources. Select this option if you're not ready to enable the rule.
    * **Report-only**: Monitor how the rule affects users without enforcing it. All attempts to access resources in the account are logged in {{site.data.keyword.atracker_short}}. Monitoring is recommended for 30 days before you enforce the rule.
1. Click **Create**.

## Creating rules by using the CLI
{: #context-restrictions-create-rules-cli}
{: cli}

To define restrictions to your cloud resources by creating rules, use the [ibmcloud cbr rule-create](/docs/iam?topic=iam-cbr-plugin#cbr-cli-rule-create-command) command. The following example creates a rule that targets the {{site.data.keyword.containershort}} and allows only private endpoints from the specified network zone to access the service.

```sh
ibmcloud cbr rule-create --description 'Example Rule Description' --service-name kms --context-attributes endpointType=private --zone-id 93de8d3f588ab2c457ff576c364d1145 --enforcement-mode report
```
{: pre}

For the `enforcement-mode` option, the CLI accepts the values `enabled`, `disabled`, and `report`. If no enforcement is specified, the rule is enabled by default. For more informaiton, see [Rule enforcement](/docs/iam?topic=iam-context-restrictions-whatis#rule-enforcement).
{: tip}

## Creating rules by using the API
{: #context-restrictions-create-rules-api}
{: api}

To create restrictions to your cloud resources by creating rules, call the [Context-based restrictions API](/apidocs/context-based-restrictions#create-rule). The following example creates an enabled rule that targets the {{site.data.keyword.containershort}} and allows requests only from the specified network zone to access the service.

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "description": "this is an example of rule", "resources": [ { "attributes": [ { "name": "accountId", "value": "12ab34cd56ef78ab90cd12ef34ab56cd" }, { "name": "serviceName", "value": "kms" } ] } ], "contexts": [ { "attributes": [ { "name": "networkZoneId", "value": "65810ac762004f22ac19f8f8edf70a34" } ] } ], "enforcement_mode": "enabled" }' "{base_url}/v1/rules"
```
{: codeblock}
{: curl}

```java
RuleContextAttribute ruleContextAttributeModel = new RuleContextAttribute.Builder()
  .name("networkZoneId")
  .value(zoneID)
  .build();
RuleContext ruleContextModel = new RuleContext.Builder()
  .attributes(java.util.Arrays.asList(ruleContextAttributeModel))
  .build();
ResourceAttribute resourceAttributeModelAccountID = new ResourceAttribute.Builder()
  .name("accountId")
  .value(accountID)
  .build();
ResourceAttribute resourceAttributeModelServiceName = new ResourceAttribute.Builder()
  .name("serviceName")
  .value(serviceName)
  .build();
ResourceTagAttribute resourceTagAttributeModel = new ResourceTagAttribute.Builder()
  .name("tagName")
  .value("tagValue")
  .build();
Resource resourceModel = new Resource.Builder()
  .addAttributes(resourceAttributeModelAccountID)
  .addAttributes(resourceAttributeModelServiceName)
  .tags(java.util.Arrays.asList(resourceTagAttributeModel))
  .build();
CreateRuleOptions createRuleOptions = new CreateRuleOptions.Builder()
  .description("this is an example of rule")
  .addContexts(ruleContextModel)
  .addResources(resourceModel)
  .enforcementMode("enabled")
  .build();

Response<Rule> response = contextBasedRestrictionsService.createRule(createRuleOptions).execute();
Rule rule = response.getResult();

System.out.println(rule);
ruleID = rule.getId();
ruleRev = response.getHeaders().values("Etag").get(0);
```
{: codeblock}
{: java}

```javascript
// Request models needed by this operation.

// RuleContextAttribute
const ruleContextAttributeModel = {
  name: 'networkZoneId',
  value: zoneId,
};

// RuleContext
const ruleContextModel = {
  attributes: [ruleContextAttributeModel],
};

// ResourceAttribute
const resourceAttributeAccountIdModel = {
  name: 'accountId',
  value: accountId,
};

// Resource Attribute
const resourceAttributeServiceNameModel = {
  name: 'serviceName',
  value: serviceName,
  operator: 'stringEquals',
};

// Resource
const resourceModel = {
  attributes: [resourceAttributeAccountIdModel, resourceAttributeServiceNameModel],
};

const params = {
  contexts: [ruleContextModel],
  resources: [resourceModel],
  description: 'this is an example of rule',
  enforcementMode: 'enabled',
};

try {
  const res = await contextBasedRestrictionsService.createRule(params);
  ruleId = res.result.id;
  ruleRev = res.headers.etag;
  console.log(JSON.stringify(res.result, null, 2));
} catch (err) {
  console.warn(err);
}
```
{: codeblock}
{: javascript}

```python
rule_context_attribute_model = {
  'name': 'networkZoneId',
  'value': zone_id,
}

rule_context_model = {
  'attributes': [rule_context_attribute_model],
}

resource_attribute_account_id_model = {
  'name': 'accountId',
  'value': account_id,
}

resource_attribute_service_name_model = {
  'name': 'serviceName',
  'value': service_name,
}

resource_model = {
  'attributes': [resource_attribute_account_id_model, resource_attribute_service_name_model],
}

rule = context_based_restrictions_service.create_rule(
  contexts=[rule_context_model],
  resources=[resource_model],
  description='this is an example of rule',
  enforcement_mode='enabled'
).get_result()

print(json.dumps(rule, indent=2))
```
{: codeblock}
{: python}

```go
ruleContextAttributeModel := &contextbasedrestrictionsv1.RuleContextAttribute{
  Name:  core.StringPtr("networkZoneId"),
  Value: core.StringPtr(zoneID),
}

ruleContextModel := &contextbasedrestrictionsv1.RuleContext{
  Attributes: []contextbasedrestrictionsv1.RuleContextAttribute{*ruleContextAttributeModel},
}

resourceModel := &contextbasedrestrictionsv1.Resource{
  Attributes: []contextbasedrestrictionsv1.ResourceAttribute{
    {
      Name:  core.StringPtr("accountId"),
      Value: core.StringPtr(accountID),
    },
    {
      Name:  core.StringPtr("serviceName"),
      Value: core.StringPtr(serviceName),
    },
  },
  Tags: []contextbasedrestrictionsv1.ResourceTagAttribute{
    {
      Name:  core.StringPtr("tagName"),
      Value: core.StringPtr("tagValue"),
    },
  },
}

createRuleOptions := contextBasedRestrictionsService.NewCreateRuleOptions()
createRuleOptions.SetDescription("this is an example of rule")
createRuleOptions.SetContexts([]contextbasedrestrictionsv1.RuleContext{*ruleContextModel})
createRuleOptions.SetResources([]contextbasedrestrictionsv1.Resource{*resourceModel})
createRuleOptions.SetEnforcementMode(contextbasedrestrictionsv1.CreateRuleOptionsEnforcementModeEnabledConst)
rule, response, err := contextBasedRestrictionsService.CreateRule(createRuleOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(rule, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}



## Creating rules by using Terraform
{: #context-restrictions-create-rules-terra}
{: terraform}

To define restrictions to your cloud resources by creating rules, use the Terraform resource [cbr_rule](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cbr_rule).

1. To install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform, follow the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a context-based restrictions rule by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

    The following example creates a rule that targets a specific {{site.data.keyword.containershort}} API and allows only private endpoints from the specified network zone to call the operations associated with that API.

    ```terraform
    resource "ibm_cbr_rule" "cbr_rule" {
      contexts {
            attributes {
                name = "endpointType"
                value = "private"
            }
      }
      description = "this is an example of rule"
      enforcement_mode = "enabled"
      operations {
            api_types {
                api_type_id = "api_type_id"
            }
      }
      resources {
            attributes {
                name = "serviceName"
                value = "containers-kubernetes"
                operator = "equals"
            }
      }
    }
    ```
    {: codeblock}
