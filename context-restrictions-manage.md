---

copyright:

  years: 2021, 2026
lastupdated: "2026-08-18"

keywords: update network access, network access rule, network zone

subcollection: iam
---

{{site.data.keyword.attribute-definition-list}}

# Managing context-based restrictions
{: #context-restrictions-update}

You can manage context rules at any time by updating the description, which helps identifying the purpose of the rule, or selecting a new list of resources and network environments. You can also remove context-based restrictions to delete restrictions that are defined by the contexts in a rule.
{: shortdesc}

Context-based restrictions can define and enforce access restrictions for its own {{site.data.keyword.cloud}} resources. You can define these restrictions based on contexts, such as network zones and endpoint types. For more information, see [What are context-based restrictions](/docs/iam?topic=iam-context-restrictions-whatis).
{: shortdesc}

The context-based restriction service manages rules and network zones, so it is possible to lose all ability to manage these resources if you cannot satisfy a rule on the context-based restriction service. Attempts to create or update such a rule are permitted only if the context of the request satisfies the new or modified rule.

If you can no longer satisfy a rule that targets the Context-based restrictions service, [open a support case](/unifiedsupport/cases/form) and provide a context that you can satisfy to restore your access.
{: tip}

## Before you begin
{: #prereqs-cbr-manage}

To manage a context-based restrictionss, you must be assigned the administrator role on the account management service.

## Updating rules by using the console
{: #context-restrictions-update-rules}
{: ui}

To edit the context-based restrictions on your cloud resources, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Rules**.
1. Select the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the rule you want to update, and select **Edit**.
1. To update the scope of APIs whose operations are restricted by your rule, select **All APIs** or **Specific APIs**. Then, click **Apply** or **Continue**.
1. To update the scope of resources for the restriction, you can select **All resources** or **Specific resources** based on the available attributes, such as resource group or location. Then, click **Apply** or **Continue**.
1. Click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") in the summary panel to update an existing context.
   1. Update the allowed endpoint types.
      - Set the toggle to No to allow all service supported endpoint types.
      - Set the toggle to Yes to allow only specific endpoint types.
   1. Update the nework zones. You can select new network zones or deselect network zones to remove them.
1. Then, click **Apply**.
1. Click the **Remove** icon ![Remove icon](../icons/delete.svg "Remove") in the summary panel to remove a context.
1. Configure a new context by selecting all endpoints or a specific endpoint, and by selecting your network zones. Then, click **Add**.
1. Click **Apply** or **Continue**.
1. Provide a new description for your rule. Click **Apply** to update the description, or click **Continue**.
1. To update the enforcement of a rule, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit"). You can **Enable**, **Disable**, or set the rule to **Report-only**.
1. Click **Apply** to finish.

## Updating rules by using the CLI
{: #context-restrictions-update-rules-cli}
{: cli}

To update the context-based restrictions on your cloud resources, use the [ibmcloud cbr rule-update](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-rule-update-command) command. The following example updates description, allowed endpoint type, and network zone for a rule with the ID `30fd58c9b75f40e854b89c432318b4a2`.
```sh
ibmcloud cbr rule-update 30fd58c9b75f40e854b89c432318b4a2 --description 'Example rule description' --service-name kms --context-attributes endpointType=private --zone-id 93de8d3f588ab2c457ff576c364d1145
```
{: pre}

## Updating rules by using the API
{: #context-restrictions-update-rules-api}
{: api}

To update restrictions to your cloud resources by creating rules, call the [Context-based restrictions API](/apidocs/context-based-restrictions?code=node#replace-rule).

1. [Get the rule](/apidocs/context-based-restrictions?code=go#get-rule) that you want to replace. In in response body, copy the rule ID and in the response headers copy the ETag header.
    ```sh
    curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "https://cbr.cloud.ibm.com/v1/rules/{rule_id}"
    ```
    {: codeblock}
    {: curl}

    ```java
    GetRuleOptions getRuleOptions = new GetRuleOptions.Builder()
    .ruleId(ruleID)
    .build();
    Response<Rule> response = contextBasedRestrictionsService.getRule(getRuleOptions).execute();
    Rule rule = response.getResult();
    System.out.println(rule);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      ruleId,
    };
    try {
      const res = await contextBasedRestrictionsService.getRule(params);
      console.log(JSON.stringify(res.result, null, 2));
    } catch (err) {
      console.warn(err);
    }
    ```
    {: codeblock}
    {: javascript}

    ```python
    rule = context_based_restrictions_service.get_rule(
      rule_id=rule_id
    )
    rule = rule.get_result()
    print(json.dumps(rule, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    getRuleOptions := contextBasedRestrictionsService.NewGetRuleOptions(
      ruleID,
    )
    rule, response, err := contextBasedRestrictionsService.GetRule(getRuleOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(rule, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

2. The following example replaces a rule with an updated version.
    The ETag value is required in the replace request’s `If-Match` header.
    {: tip}

    ```sh
    curl -X PUT --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "If-Match: {if_match}" --header "Content-Type: application/json" --data '{ "description": "this is an example of rule", "resources": [ { "attributes": [ { "name": "accountId", "value": "12ab34cd56ef78ab90cd12ef34ab56cd" }, { "name": "serviceName", "value": "kms" } ] } ], "contexts": [ { "attributes": [ { "name": "networkZoneId", "value": "76921bd873115033bd2a0909fe081b45" } ] } ], "enforcement_mode": "disabled" }' "{base_url}/v1/rules/{rule_id}"
    ```
    {: codeblock}
    {: curl}

    ```java
    RuleContextAttribute ruleContextAttributeModel = new RuleContextAttribute.Builder()
      .name("networkZoneId")
      .value("76921bd873115033bd2a0909fe081b45")
      .build();
    RuleContext ruleContextModel = new RuleContext.Builder()
      .attributes(new java.util.ArrayList<RuleContextAttribute>(java.util.Arrays.asList(ruleContextAttributeModel)))
      .build();
    ResourceAttribute resourceAttributeModel = new ResourceAttribute.Builder()
      .name("accountId")
      .value("12ab34cd56ef78ab90cd12ef34ab56cd")
      .build();
    Resource resourceModel = new Resource.Builder()
      .attributes(new java.util.ArrayList<ResourceAttribute>(java.util.Arrays.asList(resourceAttributeModel)))
      .build();
    ReplaceRuleOptions replaceRuleOptions = new ReplaceRuleOptions.Builder()
      .ruleId("testString")
      .ifMatch("testString")
      .description("this is an example of rule")
      .enforcementMode("disabled")
      .contexts(new java.util.ArrayList<RuleContext>(java.util.Arrays.asList(ruleContextModel)))
      .resources(new java.util.ArrayList<Resource>(java.util.Arrays.asList(resourceModel)))
      .build();
    Response<OutRule> response = contextBasedRestrictionsService.replaceRule(replaceRuleOptions).execute();
    OutRule outRule = response.getResult();
    System.out.println(outRule);
    ```
    {: codeblock}
    {: java}

    ```javascript
    // Request models needed by this operation.
    // RuleContextAttribute
    const ruleContextAttributeModel = {
      name: 'networkZoneId',
      value: '76921bd873115033bd2a0909fe081b45',
    };
    // RuleContext
    const ruleContextModel = {
      attributes: [ruleContextAttributeModel],
    };
    // ResourceAttribute
    const resourceAttributeModel = {
      name: 'accountId',
      value: '12ab34cd56ef78ab90cd12ef34ab56cd',
    };
    // Resource
    const resourceModel = {
      attributes: [resourceAttributeModel],
    };
    const params = {
      ruleId: 'testString',
      ifMatch: 'testString',
      contexts: [ruleContextModel],
      resources: [resourceModel],
      description: 'this is an example of rule',
      enforcementMode: 'disabled',
    };
    contextBasedRestrictionsService.replaceRule(params)
      .then(res => {
        console.log(JSON.stringify(res.result, null, 2));
      })
      .catch(err => {
        console.warn(err)
      });
    ```
    {: codeblock}
    {: javascript}

    ```python
    rule_context_attribute_model = {
      'name': 'networkZoneId',
      'value': '76921bd873115033bd2a0909fe081b45',
    }
    rule_context_model = {
      'attributes': [rule_context_attribute_model],
    }
    resource_attribute_model = {
      'name': 'accountId',
      'value': '12ab34cd56ef78ab90cd12ef34ab56cd',
    }
    resource_model = {
      'attributes': [resource_attribute_model],
    }
    out_rule = context_based_restrictions_service.replace_rule(
      rule_id='testString',
      if_match='testString',
      contexts=[rule_context_model],
      resources=[resource_model],
      description='this is an example of rule',
      enforcement_mode='disabled'
    ).get_result()
    print(json.dumps(out_rule, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    ruleContextAttributeModel := &contextbasedrestrictionsv1.RuleContextAttribute{
      Name: core.StringPtr("networkZoneId"),
      Value: core.StringPtr("76921bd873115033bd2a0909fe081b45"),
    }
    ruleContextModel := &contextbasedrestrictionsv1.RuleContext{
      Attributes: []contextbasedrestrictionsv1.RuleContextAttribute{*ruleContextAttributeModel},
    }
    resourceAttributeModel := &contextbasedrestrictionsv1.ResourceAttribute{
      Name: core.StringPtr("accountId"),
      Value: core.StringPtr("12ab34cd56ef78ab90cd12ef34ab56cd"),
    }
    resourceModel := &contextbasedrestrictionsv1.Resource{
      Attributes: []contextbasedrestrictionsv1.ResourceAttribute{*resourceAttributeModel},
    }
    replaceRuleOptions := contextBasedRestrictionsService.NewReplaceRuleOptions(
      "testString",
      "testString",
    )
    replaceRuleOptions.SetDescription("this is an example of rule")
    replaceRuleOptions.SetContexts([]contextbasedrestrictionsv1.RuleContext{*ruleContextModel})
    replaceRuleOptions.SetResources([]contextbasedrestrictionsv1.Resource{*resourceModel})
    replaceRuleOptions.SetEnforcementMode(contextbasedrestrictionsv1.ReplaceRuleOptionsEnforcementModeDisabledConst)
    outRule, response, err := contextBasedRestrictionsService.ReplaceRule(replaceRuleOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(outRule, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

## Updating network zones by using the console
{: #network-zones-update}
{: ui}

You can modify the list of allowed locations where an access request can originate. A set of one or more network locations can be specified by IP addresses (individual addresses, ranges, or subnets), VPCs, or service references. You can update a network zone that is used in a rule, or integrate the new updated network zones into your rules later.
1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Context-based restrictions**, and select **Network zones**.
1. Select the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the network zone that you want to update, and select **Edit**.
1. You can update your zone name and description.
1. You can edit the list of allowed IP addresses where an access request can originate. Include exceptions in the deny list, if necessary.
1. You can add or remove allowed VPCs.
1. You can add or remove service references. Select a service to associate its IP addresses with your network zone.
1. Click **Next** to review your new configuration.
1. To apply changes, click **Update**.

## Updating network zones by using the CLI
{: #network-zones-update-cli}
{: cli}

To update a network zone, complete the following steps.
1. Retrieve the zone ID for the network zone that you want to update by using the [ibmcloud cbr zones](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-zones-command) command to list all zones in the account.
    ```sh
    ibmcloud cbr zones
    ```
    {: pre}

1. Update the network zone by using the [ibmcloud cbr zone-update](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-zone-update-command) command. The following example updates the zone name, allowed addresses, and excluded addresses for a network zone with the ID `65810ac762004f22ac19f8f8edf70a34`.
    ```sh
    ibmcloud cbr zone-update 65810ac762004f22ac19f8f8edf70a34 --name 'Example Zone Name' --addresses 166.22.23.0-166.22.23.108 --excluded 166.22.23.100
    ```
    {: pre}

## Updating network zones by using the API
{: #network-zones-update-api}
{: api}

To update a network zone, complete the following steps.
1. [Get the zone](/apidocs/context-based-restrictions?code=go#get-zone) that you want to replace. In the response body, copy the zone ID and in the response headers copy the ETag header.
    ```sh
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "https://cbr.cloud.ibm.com/v1/zones/{zone_id}"
   ```
   {: codeblock}
   {: curl}

    ```java
   GetZoneOptions getZoneOptions = new GetZoneOptions.Builder()
     .zoneId(zoneID)
     .build();
    Response<Zone> response = contextBasedRestrictionsService.getZone(getZoneOptions).execute();
   Zone zone = response.getResult();
    System.out.println(zone);
   ```
   {: codeblock}
   {: java}

    ```javascript
   const params = {
     zoneId,
   };
   try {
     const res = await contextBasedRestrictionsService.getZone(params);
     console.log(JSON.stringify(res.result, null, 2));
   } catch (err) {
     console.warn(err);
   }
   ```
   {: codeblock}
   {: javascript}

    ```python
   get_zone_response = context_based_restrictions_service.get_zone(
     zone_id=zone_id
   )
   zone = get_zone_response.get_result()
    print(json.dumps(zone, indent=2))
   ```
   {: codeblock}
   {: python}

   ```go
   getZoneOptions := contextBasedRestrictionsService.NewGetZoneOptions(
     zoneID,
   )
    zone, response, err := contextBasedRestrictionsService.GetZone(getZoneOptions)
   if err != nil {
     panic(err)
   }
   b, _ := json.MarshalIndent(zone, "", "  ")
   fmt.Println(string(b))
   ```
   {: codeblock}
   {: go}

2.  Update the network zone by using the [Replace zone](/apidocs/context-based-restrictions?code=go#replace-zone) method.
    The ETag value is required in the replace request’s `If-Match` header.
    {: tip}

    ```sh
    curl -X PUT --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "If-Match: {if_match}" --header "Content-Type: application/json" --data '{ "name": "new zone name", "description": "new zone description", "account_id": "12ab34cd56ef78ab90cd12ef34ab56cd", "addresses": [ { "type": "ipAddress", "value": "169.23.56.234" }, { "type": "ipRange", "value": "169.23.22.0-169.23.22.255" }, { "type": "vpc", "value": "crn:v1:bluemix:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r134-d98a1702-b39a-449a-86d4-ef8dbacf281e" } ] }' "{base_url}/v1/zones/{zone_id}"
    ```
    {: codeblock}
    {: curl}

    ```java
    AddressIPAddress addressModel = new AddressIPAddress.Builder()
      .type("ipAddress")
      .value("169.23.56.234")
      .build();
    ReplaceZoneOptions replaceZoneOptions = new ReplaceZoneOptions.Builder()
      .zoneId("testString")
      .ifMatch("testString")
      .name("an example of zone")
      .accountId("12ab34cd56ef78ab90cd12ef34ab56cd")
      .description("this is an example of zone")
      .addresses(new java.util.ArrayList<Address>(java.util.Arrays.asList(addressModel)))
      .build();
    Response<OutZone> response = contextBasedRestrictionsService.replaceZone(replaceZoneOptions).execute();
    OutZone outZone = response.getResult();
    System.out.println(outZone);
    ```
    {: codeblock}
    {: java}

    ```javascript
    // Request models needed by this operation.
    // AddressIPAddress
    const addressModel = {
      type: 'ipAddress',
      value: '169.23.56.234',
    };
    const params = {
      zoneId: 'testString',
      ifMatch: 'testString',
      name: 'an example of zone',
      accountId: '12ab34cd56ef78ab90cd12ef34ab56cd',
      addresses: [addressModel],
      description: 'this is an example of zone',
    };
    contextBasedRestrictionsService.replaceZone(params)
      .then(res => {
        console.log(JSON.stringify(res.result, null, 2));
      })
      .catch(err => {
        console.warn(err)
      });
    ```
    {: codeblock}
    {: javascript}

    ```python
    address_model = {
      'type': 'ipAddress',
      'value': '169.23.56.234',
    }
    out_zone = context_based_restrictions_service.replace_zone(
      zone_id='testString',
      if_match='testString',
      name='an example of zone',
      account_id='12ab34cd56ef78ab90cd12ef34ab56cd',
      addresses=[address_model],
      description='this is an example of zone'
    ).get_result()
    print(json.dumps(out_zone, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    addressModel := &contextbasedrestrictionsv1.AddressIPAddress{
      Type: core.StringPtr("ipAddress"),
      Value: core.StringPtr("169.23.56.234"),
    }
    replaceZoneOptions := contextBasedRestrictionsService.NewReplaceZoneOptions(
      "testString",
      "testString",
    )
    replaceZoneOptions.SetName("an example of zone")
    replaceZoneOptions.SetAccountID("12ab34cd56ef78ab90cd12ef34ab56cd")
    replaceZoneOptions.SetDescription("this is an example of updated zone")
    replaceZoneOptions.SetAddresses([]contextbasedrestrictionsv1.AddressIntf{addressModel})
    outZone, response, err := contextBasedRestrictionsService.ReplaceZone(replaceZoneOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(outZone, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

## Removing a rule by using the console
{: #context-restrictions-remove-rules}
{: ui}

Deleting rules removes context-based restrictions from the given resource, and requests from any context are allowed if the user has the correct permissions.
You can remove a rule on your cloud resources by completing the following steps:
1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Context-based restrictions**, and select **Rules**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") in the row that contains the rule, and click **Remove**.

## Removing a rule by using the CLI
{: #context-restrictions-remove-rules-cli}
{: cli}

You can remove a rule on your cloud resources by completing the following steps:
1. Retrieve the rule ID for the rule that you want to delete by using the [context-based restrictions rules](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-rules-command) command. You can narrow the results of the list by specifying attributes as command options.
   ```sh
   ibmcloud cbr rules --service-name "iam-identity"
   ```
   {: pre}

   You can also filter by service group ID:
   ```sh
   ibmcloud cbr rules --service-group-id iam
   ```
   {: pre}

1. Delete the rule for the specified rule ID by using the [cbr rule-delete](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-rule-delete-command) command.
   ```sh
   ibmcloud cbr rule-delete 30fd58c9b75f40e854b89c432318b4a2
   ```
   {: pre}

## Removing a rule by using the API
{: #context-restrictions-remove-rules-api}
{: api}

You can remove a rule on your cloud resources by completing the following steps:
1. Retrieve the rule ID for the rule that you want to delete by using the [context-based-restrictions list rules](/apidocs/context-based-restrictions#list-rules) method.
   ```sh
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/rules?account_id={account_id}"
   ```
   {: codeblock}
   {: curl}

   ```java
   ListRulesOptions listRulesOptions = new ListRulesOptions.Builder()
   .accountId("testString")
   .build();

   Response<OutRulePage> response = contextBasedRestrictionsService.listRules(listRulesOptions).execute();
   OutRulePage outRulePage = response.getResult();

   System.out.println(outRulePage);
   ```
   {: codeblock}
   {: java}

   ```javascript
    const params = {
      accountId: 'testString',
    };

    contextBasedRestrictionsService.listRules(params)
      .then(res => {
        console.log(JSON.stringify(res.result, null, 2));
      })
      .catch(err => {
        console.warn(err)
      });
   ```
   {: codeblock}
   {: javascript}

   ```python
   out_rule_page = context_based_restrictions_service.list_rules(
      account_id='testString'
    ).get_result()

    print(json.dumps(out_rule_page, indent=2))
   ```
   {: codeblock}
   {: python}

   ```go
    listRulesOptions := contextBasedRestrictionsService.NewListRulesOptions(
      "testString",
    )

    ruleList, response, err := contextBasedRestrictionsService.ListRules(listRulesOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(ruleList, "", "  ")
    fmt.Println(string(b))
   ```
   {: codeblock}
   {: go}

1. Delete the rule for the specified rule ID.
   ```sh
   curl -X DELETE --location --header "Authorization: Bearer {iam_token}" "{base_url}/v1/rules/{rule_id}"
   ```
   {: codeblock}
   {: curl}

   ```java
   DeleteRuleOptions deleteRuleOptions = new DeleteRuleOptions.Builder()
     .ruleId("testString")
     .build();

   Response<Void> response = contextBasedRestrictionsService.deleteRule(deleteRuleOptions).execute();
   ```
   {: codeblock}
   {: java}

   ```javascript
    const params = {
      ruleId: 'testString',
    };

    contextBasedRestrictionsService.deleteRule(params)
      .then(res => {
        done();
      })
      .catch(err => {
        console.warn(err)
      });
   ```
   {: codeblock}
   {: javascript}

   ```python
    response = context_based_restrictions_service.delete_rule(
      rule_id='testString'
    )
   ```
   {: codeblock}
   {: python}

   ```go
    deleteRuleOptions := contextBasedRestrictionsService.NewDeleteRuleOptions(
      "testString",
    )

    response, err := contextBasedRestrictionsService.DeleteRule(deleteRuleOptions)
    if err != nil {
      panic(err)
    }
    if response.StatusCode != 204 {
      fmt.Printf("\nUnexpected response status code received from DeleteRule(): %d\n", response.StatusCode)
    }
   ```
   {: codeblock}
   {: go}

## Removing a network zone by using the console
{: #network-zones-remove}
{: ui}

Removing a network zone removes the set of allowed network locations from which an access request is created. If a network zone is added to a rule, you first have to remove the zone from the rule. Complete the following steps to remove a network zone:
1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Context-based restrictions**, and select **Network zones**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") in the row that contains the network zone, and click **Remove**.

## Removing a network zone by using the CLI
{: #network-zones-remove-cli}
{: cli}

Removing a network zone removes the set of allowed network locations from which an access request is created. If a network zone is added to a rule, you first have to remove the zone from the rule. For more information about removing a zone from a rule, see [Updating context-based restrictions](/docs/iam?topic=iam-context-restrictions-update) . Then, complete the following steps:
1. Retrieve the zone ID for the network zone that you want to delete by using the [contxt-based restrictions zones](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-zones-command) command. You can narrow the results of the list by specifying the name of the zone.
   ```sh
   ibmcloud cbr zones --name "Example zone"
   ```
   {: pre}

1. Delete the network zone for the specified zone ID by using the [cbr zone-delete](/docs/iam?topic=iam-cbr-plugin&interface=cli#cbr-cli-zone-delete-command) command.
   ```sh
   ibmcloud cbr zone-delete 65810ac762004f22ac19f8f8edf70a34
   ```
   {: pre}

## Removing a network zone by using the API
{: #network-zones-remove-api}
{: api}

Removing a network zone removes the set of allowed network locations from which an access request is created. If a network zone is added to a rule, you first have to remove the zone from the rule. See [Updating context-based restrictions](/docs/iam?topic=iam-context-restrictions-update) for more information about removing a zone from a rule. Then, complete the following steps:
1. Retrieve the rule ID for the rule that you want to delete by using the [Context-based restrictions list zones](/apidocs/context-based-restrictions#list-zones) method.
   ```sh
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/zones?account_id={account_id}"
   ```
   {: codeblock}
   {: curl}

   ```java
   ListZonesOptions listZonesOptions = new ListZonesOptions.Builder()
   .accountId("testString")
   .build();

   Response<OutZonePage> response = contextBasedRestrictionsService.listZones(listZonesOptions).execute();
   OutZonePage outZonePage = response.getResult();

   System.out.println(outZonePage);
   ```
   {: codeblock}
   {: java}

   ```javascript
    const params = {
      accountId: 'testString',
    };

    contextBasedRestrictionsService.listZones(params)
      .then(res => {
        console.log(JSON.stringify(res.result, null, 2));
      })
      .catch(err => {
        console.warn(err)
      });
   ```
   {: codeblock}
   {: javascript}

   ```python
    out_zone_page = context_based_restrictions_service.list_zones(
      account_id='testString'
    ).get_result()

    print(json.dumps(out_zone_page, indent=2))
   ```
   {: codeblock}
   {: python}

   ```go
    listZonesOptions := contextBasedRestrictionsService.NewListZonesOptions(
      "testString",
    )

    outZonePage, response, err := contextBasedRestrictionsService.ListZones(listZonesOptions)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(outZonePage, "", "  ")
    fmt.Println(string(b))
   ```
   {: codeblock}
   {: go}

1. Delete the network zone for the specified zone ID.
   ```sh
   curl -X DELETE --location --header "Authorization: Bearer {iam_token}" "{base_url}/v1/zones/{zone_id}"
   ```
   {: codeblock}
   {: curl}

   ```java
    DeleteZoneOptions deleteZoneOptions = new DeleteZoneOptions.Builder()
      .zoneId("testString")
      .build();

    Response<Void> response = contextBasedRestrictionsService.deleteZone(deleteZoneOptions).execute();
   ```
   {: codeblock}
   {: java}

   ```javascript
    const params = {
      zoneId: 'testString',
    };

    contextBasedRestrictionsService.deleteZone(params)
      .then(res => {
        done();
      })
      .catch(err => {
        console.warn(err)
      });
   ```
   {: codeblock}
   {: javascript}

   ```python
    response = context_based_restrictions_service.delete_zone(
      zone_id='testString'
    )
   ```
   {: codeblock}
   {: python}

   ```go
    deleteZoneOptions := contextBasedRestrictionsService.NewDeleteZoneOptions(
      "testString",
    )

    response, err := contextBasedRestrictionsService.DeleteZone(deleteZoneOptions)
    if err != nil {
      panic(err)
    }
    if response.StatusCode != 204 {
      fmt.Printf("\nUnexpected response status code received from DeleteZone(): %d\n", response.StatusCode)
    }
   ```
   {: codeblock}
   {: go}

## Restricting the ability to manage rules and network zones by using the console
{: #cbr-rules-ui}
{: ui}

To configure this rule, target the **Context-based restrictions** service. For more information about the steps to set up a rule, see [Creating rules](/docs/iam?topic=iam-context-restrictions-create&interface=ui#context-restrictions-create-rules).
A rule scoped to **All resources** is applicable to all current and future resources that are managed by the service. If you want to restrict operations for a specific resource, scope the rule to **Specific resources > Resource type**.
To complete any rule or network zone management operation, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restrictions rule.
{: note}

## Restricting the ability to manage rules and network zones by using the API
{: #cbr-rules-api}
{: api}

The following example shows a rule in JSON format that protects rule and network zone management operations:
```json
{
  "resources": [
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "my-AccountID"
        },
        {
          "name": "serviceName",
          "value": "context-based-restrictions"
        }
      ]
    }
  ],
  "description": "",
  "contexts": [
    {
      "attributes": [
        {
          "name": "networkZoneId",
          "value": "my-zoneID"
        }
      ]
    }
  ],
  "enforcement_mode": "report"
}
```
{: curl}
{: codeblock}

A rule that specifies only the `accountId` and `serviceName` resource attributes is applicable to all current and future resources that are managed by the service. If you want to restrict operations for a specific resource, include the corresponding `resourceType` resource attribute.  Valid `resourceType` values for the Context-based restrictions service are `rule` and `zone`.

To complete any rule or network zone management operation, a user must be assigned the correct role with an IAM access policy and they must satisfy the context-based restrictions rule.
{: note}
