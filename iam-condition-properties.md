---

copyright:

  years: 2022, 2026
lastupdated: "2026-03-23"

keywords: trusted profile, dynamic rule, operators, rules, conditions, properties, time-based, resource attribute

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# IAM condition properties
{: #iam-condition-properties}

Dynamic rules and trusted profiles both use conditional IAM statements that you specify to automatically add federated users to access groups or trusted profiles. When users log in with a federated ID, the data from the identity provider (IdP) dynamically maps them to an access group based on conditions that you set. For more information, see [Creating dynamic rules for access groups](/docs/account?topic=account-rules) and [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).

You can also assign conditional IAM access policies to designate temporary access to resources in your account or allow access to resources during specific time windows. For more information, see [Limiting access with time-based conditions](/docs/iam?topic=iam-iam-time-based) and review the section [Conditions in `/v2/policies` access policies](/docs/iam?topic=iam-iam-condition-properties#policy-condition-properties).

## Dynamic rule and trusted profile details
{: #general-details}

Each dynamic rule and trusted profile trust relationship has the following properties:

Name
:   Enter a custom name that helps you remember what type of users you are adding to an access group or trusted profile.

Identity provider (IdP)
:   The dynamic rule or trusted profile is evaluated only if the user who is logging in authenticates by using the enterprise IdP with this issuer URI. Your IdP URL is displayed in the console for you to copy and paste when you create a dynamic rule or trusted profile. For example, `https://w3id.sso.ibm.com/auth/sps/samlidp2/saml20`. You can also view th IdP by clicking `View identity provider (IdP) data`. For IBMid, the IdP is the SAML "entityId" field, sometimes referred to as the issuer ID, and is part of the federation configuration when you are onboarding with IBMid. For App ID, equivalent syntax is the "realm ID". For more information, see [Enabling authentication from an external identity provider](/docs/account?topic=account-ibm-idp-integration)

Session duration
:   The dynamic access group membership or trusted profile session expires after the number of hours that are specified in this property. For example, if the property is set to 24 hours, the user’s dynamic or trusted profile session ends one day (24 hours) after they log in.

### Rule and profile condition statement properties
{: #condition-properties}

Additionally, each dynamic rule and trusted profile trust relationship has one or more conditions that consist of the following properties. Users need to satisfy all conditions for the overall dynamic rule or trusted profile authentication to evaluate to true:

Allow users when
: An attribute name that is part your identity provider data. To learn more about how attribute names are created from your enterprise identity provider to the condition evaluation, see [Mapping of enterprise identity provider attributes](https://developer.ibm.com/articles/identity-and-access-management-what-developers-need-to-know/#mapping-of-enterprise-identity-provider-attributes){: external}.

Operator
:   Compares the attribute that is specified in the `Allow users when` field with the `Values` property. You can choose from Equals, Not Equals, Equals Ignore Case, Not Equals Ignore Case, In, and Contains. Use the Contains option when the attribute statement has an array type. You can enter more than one value to be matched by using the In option.

Values
:   An attribute value that is used by the comparator to evaluate against the `Allow users when` attribute name.

You can think of a dynamic rule or trusted profile condition as a key:value pair. The key is what you add in the `Allow users when` field, and the value is what you enter in the `Values` field.
{: tip}

### Available operators for rule and profile conditions
{: #operators}

| Operator | Description  | Sample condition |
|------------|--------------|------------------|
| Equals                 | Case-sensitive string comparison. Boolean or number values are converted into a string before comparison. | primaryGroup Equals “Admins” |
| Not Equals             | Negated case-sensitive string comparison. Boolean or number values are converted into a string before comparison. | primaryGroup NotEquals “Admins” |
| Equals Ignore Case     | Case-insensitive string comparison. Boolean or number values are converted into a string before comparison. | isManager EqualsIgnoreCase “tRuE” |
| Not Equals Ignore Case | Negated case-insensitive string comparison. Boolean or number values are converted into a string before comparison.	 | is_teamlead NotEqualsIgnoreCase “TrUe” |
| Contains               | If the attribute is an array of strings, numbers, or Booleans, `Contains` determines by using the comparator `Equals` if the value that is provided is part of the array in the login message. If the attribute is a single string instead, `Contains` determines whether the value that is provided is contained in the string attribute in the login message. | `group` contains “Admins” |
| In                     | Short notation for multiple Equal operators. Compares the value in the login message attribute with the list of potential values in this rule. Boolean or numbers are converted to a string before comparison. | jobRole in [“Manager”,”Director”,”Team-Lead”] |
{: caption="Available operators for conditions" caption-side="top"}

#### Example
{: #example-values}

The following table includes values for each of the fields for a dynamic rule or a trusted profile condition. In this example, users who are identified as managers within the federated IdP are mapped to an {{site.data.keyword.cloud_notm}} access group or trusted profile that has specific access set for only managers.

| Field                           | Value                           |
|---------------------------------|---------------------------------|
| Name                            | `Manager`                         |
| Identity provider               | `https://idp.example.org/SAML2` |
| Session duration in hours       | `12`                              |
| Allow users when (attribute name) | `isManager`                       |
| Operator                      | `Equals`                          |
| Value                           | `true`                            |
{: caption="Example values" caption-side="top"}

### Compute resource attribute names
{: #cr-attribute-names}

To establish trust with a compute resource in a trusted profile, you can use the {{site.data.keyword.cloud_notm}} console, {{site.data.keyword.cloud_notm}} CLI, or the IAM API. If you select **All service resources** and add conditions to filter the compute resource instances that can apply the profile, the conditions are built based on the following resource attributes.

#### Kubernetes and Red Hat OpenShift attribute names
{: #cr-kub-rhos}

| {{site.data.keyword.cloud_notm}} console name | CLI and API name | Description         |
|---------------------------------|---------------------------------|---------------------|
| Resource group ID      | `resource_group_id` | The ID of the resource group that contains this cluster. You can identify the resource group of a cluster by using its overview page in the IBM Cloud Console. |
| Resource group name    | `resource_group_name` | The name of the resource group that contains this cluster. |
| Service instance       | `service_instance`    | The ID of this cluster. You can retrieve this value from the cluster's overview page in the IBM Cloud Console as "Cluster ID" or using the IBM Cloud CLI. |
| Location               | `location`            | Location of the cluster derived from its cloud resource name. |
| Namespace              | `namespace`           | Namespace of the service account that is used to retrieve a Compute Resource token and get an IAM token. |
| Service account        | `name`                | Name of the service account that is used to retrieve a Compute Resource token and get an IAM token. |
| Pod                    | `pod`                 | The name of the Kubernetes pod that runs the code that wants to retrieve an IAM token. |
{: caption="Kubernetes and Red Hat OpenShift attribute names" caption-side="top"}

#### Virtual server for VPC attribute names
{: #cr-vpc}

| {{site.data.keyword.cloud_notm}} console name | CLI and API name | Description         |
|---------------------------------|---------------------------------|---------------------|
| Resource group ID      | `resource_group_id`   | The ID of the resource group that contains this cluster. You can identify the resource group of a cluster by using its overview page in the IBM Cloud Console. |
| Resource group name    | `resource_group_name` | The name of the resource group that contains this cluster. |
| Resource ID            | `resource`            | The ID of the virtual server for VPC. |
| Instance group name    | `instance_group_name` | Name of the instance group, if this virtual server is part of one. |
| Region                 | `region`              | Region into which this virtual server is deployed. |
| Subnet                 | `subnet_id`           | The subnet ID of the virtual server for VPC, if one is available. |
| VPC ID                 | `vpc_id`              | The VPC ID of the virtual server for VPC, if one is available. |
| Zone                   | `zone`                | Zone name in which this virtual server is deployed to. |
{: caption="Virtual server for VPC attribute names" caption-side="top"}

### {{site.data.keyword.cloud_notm}} CLI command examples
{: #cr-rule-cli-examples}

The following examples show how you can use the attribute names in the CLI to build trusted profile links and conditions.

#### Linking a trusted profile to Kubernetes a cluster
{: #tp-link-cluster}

To link the trusted profile `Test` to the Kubernetes cluster `c0pigdctkkc07fs7pm06` in the account `444aebb0657c7f0f3aae8e7bdc78709a` and service account `my-service-account` in the namespace `my-namespace`, specify the following command:

```bash
ibmcloud iam trusted-profile-link-create Test --name NewLink4IKS --cr-type IKS_SA \
               --link-crn 
crn:v1:bluemix:public:containers-kubernetes:us-east:a/444aebb0657c7f0f3aae8e7bdc78709a:c0pigdctkkc07fs7pm06:: \
              --link-namespace "my-namespace" \
              --link-name "my-service-account"
```
{: pre}

#### Creating trusted profile conditions for Kubernetes
{: #tp-condition-cluster}

To connect the trusted profile with the ID `Profile-b2f13064-2b8c-4e4b-9181-c1973a408e3c` to all service accounts in the Kubernetes cluster `c0pigdctkkc07fs7pm06` in the account `444aebb0657c7f0f3aae8e7bdc78709a` and the service account namespace `my-namespace`, specify the following command:

```bash
ibmcloud iam trusted-profile-rule-create Profile-b2f13064-2b8c-4e4b-9181-c1973a408e3c \
              --name NewRule4IKS --type Profile-CR --cr-type IKS_SA \
               --conditions "claim:service_instance,operator:EQUALS,vlaue:c0pigdctkkc07fs7pm06" \
               --conditions "claim:namespace,operator:EQUALS,value:my-namespace"
```
{: pre}

#### Creating trusted profile conditions for VPC
{: #tp-condition-vpc}

To connect the trusted profile with the ID `Profile-b2f13064-2b8c-4e4b-9181-c1973a408e3c` to all virtual servers in one VPC `r206-1db73eed-b0fb-b04f-bb57-4d3a3c2dff9d` in the account `444aebb0657c7f0f3aae8e7bdc78709a`, specify the following command:

```bash
ibmcloud iam trusted-profile-rule-create Profile-b2f13064-2b8c-4e4b-9181-c1973a408e3c \
              --name NewRule4VSI --type Profile-CR --cr-type VSI \
               --conditions "claim:vpc_id,operator:EQUALS,value:r206-1db73eed-b0fb-b04f-bb57-4d3a3c2dff9d"
```
{: pre}

## Conditions in `v2` access policies
{: #policy-condition-properties}

Time-based and resource attribute-based conditions for IAM access policies use `/v2/policies` syntax. Policies that use `/v1/policies` syntax aren't eligible to add time-based resource attribute-based conditions. For more information, see [Access policy version limitations](/docs/account?topic=account-known-issues#policy-version-limit).

To view the new schema for policies, see [/v2/policies](/docs/account?topic=account-known-issues&interface=ui#v2-policies).

### Time-based conditions
{: #time-based-conditions}

The following table lists the operators available for creating time-based conditions for access policies.

| Operator   | Description  | Example |
|------------|--------------|---------|
| `dayOfWeekAnyOf` | The days of the week that the client can use the policy.   \n 1 - Monday   \n 2 - Tuesday   \n 3 - Wednesday   \n 4- Thursday   \n 5 - Friday   \n 6 - Saturday   \n 7 - Sunday | See [example](/docs/iam?topic=iam-iam-condition-properties#dayOfWeekAnyOf-timeGreaterThanOrEquals-timeLessThanOrEquals). |
| `timeGreaterThanOrEquals` | The time that the condition begins granting access. Time is calculated by `<time>±<time_zone_offset>`. | See [example](/docs/iam?topic=iam-iam-condition-properties#dayOfWeekAnyOf-timeGreaterThanOrEquals-timeLessThanOrEquals). |
| `timeLessThanOrEquals` | The time that the condition terminates access. Time is calculated by `<time>±<time_zone_offset>`. | See [example](/docs/iam?topic=iam-iam-condition-properties#dayOfWeekAnyOf-timeGreaterThanOrEquals-timeLessThanOrEquals). |
| `dateTimeGreaterThanOrEquals` | The date and time that the condition begins granting access. Date is calculated by `<datetime>±<time_zone_offset>`. |  See [example](/docs/iam?topic=iam-iam-condition-properties#dateTimeGreaterThanOrEquals-dateTimeLessThanOrEquals). |
| `dateTimeLessThanOrEquals` | The date and time that the condition terminates access. Date is calculated by `<datetime>±<time_zone_offset>`. | See [example](/docs/iam?topic=iam-iam-condition-properties#dateTimeGreaterThanOrEquals-dateTimeLessThanOrEquals). |
{: caption="The operators available to time-based conditions for access policies." caption-side="top"}

When you define a condition with a `GreaterThanOrEquals` operator, always include a condition with a `LessThanOrEquals` operator. This way, there is a clearly defined duration, whether it is temporary, recurring all day, or recurring with custom hours. For more information, see [Condition patterns](/docs/iam?topic=iam-iam-time-based#advanced-condition-service).

For date and time operators, policies support the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format `hh:mm:ss±hh:mm`. The time zone offset refers to Coordinated Universal Time.
{: note}

Use the following variables to represent the `key` that specifies the client’s environment attribute, which the policy evaluates against. Each `key` supports a discrete set of operators.

| Variable name | Description | Supported operators |
|---------------|-------------|----------------------|
| `environment.attributes.current_time` | The client's current time. | `timeGreaterThanOrEquals`, `timeLessThanOrEquals` |
| `environment.attributes.current_date_time` | The client's current date and time. | `dateTimeGreaterThanOrEquals`, `dateTimeLessThanOrEquals` |
| `environment.attributes.day_of_week` | The client's current day of the week. | `dayOfWeekAnyOf`, `dayOfWeekEquals` |
{: caption="Variable notation for time-based conditions." caption-side="top"}

#### Example: dayOfWeekAnyOf, timeGreaterThanOrEquals, and timeLessThanOrEquals
{: #dayOfWeekAnyOf-timeGreaterThanOrEquals-timeLessThanOrEquals}

The days of the week that are specified in this example map to Monday, Tuesday, Wednesday, and Thursday. The `timeGreaterThanOrEquals` value indicates that the condition begins granting access at 9 AM in the time zone UTC-5. The `timeLessThanOrEquals` value indicates that the condition terminates access at 5 PM in the time zone UTC-5.`environment.attributes.current_time` and `environment.attributes.day_of_week` indicate that it is a [recurring time-based condition](/docs/iam?topic=iam-iam-time-based#iam-time-based-recur-ui). Always include `time` conditions with a `dayOfWeek` condition.

```json
"conditions": [
			{
				"key": "{{environment.attributes.day_of_week}}",
				"operator": "dayOfWeekAnyOf",
				"value": [
					1,
					2,
					3,
					4
				]
			},
			{
				"key": "{{environment.attributes.current_time}}",
				"operator": "timeGreaterThanOrEquals",
				"value": "09:00:00-05:00"
			},
			{
				"key": "{{environment.attributes.current_time}}",
				"operator": "timeLessThanOrEquals",
				"value": "17:00:00-05:00"
			}
		]
```
{: codeblock}

#### Example: dayOfWeekEquals
{: #dayOfWeekEquals}

The day of the week in this example is represented by `3` in the `value` string, which maps to Wednesday. In that same string, `+6:00` represents the time zone `UTC+6:00`. There's only one condition, so it's nested under `"rule"`.

```json
"rule": {
		"key": "{{environment.attributes.day_of_week}}",
		"operator": "dayOfWeekEquals",
		"value": "3+06:00"
},
```
{: codeblock}

#### Example: dateTimeGreaterThanOrEquals and dateTimeLessThanOrEquals
{: #dateTimeGreaterThanOrEquals-dateTimeLessThanOrEquals}

In this example, the `dateTimeGreaterThanOrEquals` value indicates that the condition begins granting access on 26 December 2022 at 9 AM in the UTC-5 time zone. The `dateTimeLessThanOrEquals` value indicates that the condition terminates access on 27 December 2022 at 5 PM in the UTC-5 time zone. `environment.attributes.current_date_time` indicates that it is a [temporary time-based condition](/docs/iam?topic=iam-iam-time-based#iam-time-based-recur-ui).

```json
"conditions": [
			{
				"key": "{{environment.attributes.current_date_time}}",
				"operator": "dateTimeGreaterThanOrEquals",
				"value": "2022-12-26T09:00:00-05:00"
			},
			{
				"key": "{{environment.attributes.current_date_time}}",
				"operator": "dateTimeLessThanOrEquals",
				"value": "2022-12-27T17:00:00-05:00"
			}
		]
```
{: codeblock}

### Resource attribute-based conditions
{: #resource-based-conditions}

The following table lists the operators available for creating resource attribute-based conditions for access policies.

| Operator   | Description  | Example |
|------------|--------------|---------|
| `stringEquals`  | Case-sensitive string comparison. Boolean or number values are converted into a string before comparison. | See [example](/docs/iam?topic=iam-iam-condition-properties#example-stringExists).|
| `stringExists` | Boolean where `true` indicates that the string must be present and can be empty. `false` indicates that the string must not be present.| See [example](/docs/iam?topic=iam-iam-condition-properties#example-stringExists). |
| `stringMatch`  | Case-sensitive string match is performed between the pattern and the target string by using either an asterisk (`*`), question mark (`?`), both, or none (same as literal value). An asterisk (`*`) represents any sequence of zero or more characters in the string, and a question mark (`?`) represents any single character. You can also express an asterisk `*` and question mark `?` as a literal value by enclosing each within two sets of curly brackets `{{}}`. |  See [example](/docs/iam?topic=iam-iam-condition-properties#example-stringExists). |
| `stringEqualsAnyOf` | Case-sensitive exact string matching any of the strings in an array of strings. Limit of 10 values. |  See [example](/docs/iam?topic=iam-iam-condition-properties#example-stringMatchAnyOf-stringEqualsAnyOf). |
| `stringMatchAnyOf` | Case-sensitive string matching any of the strings in an array of strings. The string values can include either an asterisk (`*`), question mark (`?`), both, or none (same as literal value). An asterisk (`*`) represents any sequence of zero or more characters in the string, and a question mark (`?`) represents any single character. You can also express an asterisk `*` and question mark `?` as a literal value by enclosing each within two sets of curly brackets `{{}}`. Limit of 10 values. |
{: caption="The operators available to resource attribute-based conditions for access policies." caption-side="top"}

The `key` represents the resource attribute that is supported by the chosen service. A `key` takes the form of `resource.attributes.<attribute-name>`. For example, in the case of Cloud Object Storage, the supported `prefix` attribute can be represented as the key with the `resource.attributes.prefix` notation. The following table lists example variables and is not all inclusive.

| Variable name | Description | Supported operators |
|---------------|-------------|----------------------|
| `resource.attributes.prefix` | Defines the prefix that this condition should allow for listing objects or folders. | `stringMatchAnyOf` |
| `resource.attributes.path` | Scopes all read, write, and management access on objects. | `stringMatchAnyOf` |
| `resource.attributes.delimiter` | Restricts the type of folder structure that the user can generate and helps the user navigate the bucket like a file hierarchy.   | `stringEquals` |
{: caption="Variable notation for resource attribute-based conditions." caption-side="top"}

For more information, see [Condition patterns](/docs/iam?topic=iam-iam-time-based).

#### Example: stringMatchAnyOf and stringEqualsAnyOf
{: #example-stringMatchAnyOf-stringEqualsAnyOf}

In this example, the `stringMatchAnyOf` values for the `resource.attributes.path` variable indicates that access is granted when the object path matches and begins with either `home/David/*`, `special/*`, `restricted/*`, or `temporary/test*spatial.?.log` (e.g. temporary/test_spatial.1.log). The `or` value indicates that there is an alternative condition that can grant access.

The `stringEqualsAnyOf` value for the `resource.attributes.delimiter` variable indicates that access is granted when there is no boundary indicator or when `/` is present. Additionally, the `stringEqualsAnyOf`for the `resource.attributes.prefix` variable indicates that `home/`, or `home/David/`, or no prefix must also exist to grant access. The `and` value let's us know that both the `resource.attributes.delimiter` and `resource.attributes.prefix` must be met to grant access.

```json
"pattern": "attribute-based-condition:resource:literal-and-wildcard",
"rule": {
    "operator": "or",
    "conditions": [
      {
        "key": "{{resource.attributes.path}}",
        "operator": "stringMatchAnyOf",
        "value": [
          "home/David/*",
          "special/*",
          "restricted/*",
          "temporary/test*spatial.?.log"
        ]
      },
      {
        "operator": "and",
        "conditions": [
          {
            "key": "{{resource.attributes.delimiter}}",
            "operator": "stringEqualsAnyOf",
            "value": [
              "",
              "/"
            ]
          },
          {
            "key": "{{resource.attributes.prefix}}",
            "operator": "stringEqualsAnyOf",
            "value": [
              "",
              "home/",
              "home/David/"
            ]
          }
        ]
      }
    ]
  }
```
{: codeblock}

#### Example: stringExists, stringEquals, stringMatch
{: #example-stringExists}

In this example, `stringEquals` for `iam_id`, `accountID`, `serviceName`, and `resourceType` indicates that an exact string match is performed. The asterisk present in the `stringMatch` value for the resource variable indicates that access is granted to all resources that begin with `dev-bucket-`. The true `stringExists` value for the path variable and the `false` stringExists value for the prefix and delimiter variable indicates that only the path must exist to grant access.

```json
{
    "type": "access",
    "subject": {
        "attributes": [
            {
                "key": "iam_id",
                "operator": "stringEquals",
                "value": "IBMid-1234"
            }
        ]
    },
    "control": {
        "grant": {
            "roles": [
                {
                    "role_id": "crn:v1:bluemix:public:cloud-object-storage::::role:ListFolderContent"
                },
                {
                    "role_id": "crn:v1:bluemix:public:cloud-object-storage::::role:ListFolder"
                },
                {
                    "role_id": "crn:v1:bluemix:public:cloud-object-storage::::role:AllFolderOperations"
                }
            ]
        }
    },
    "resource": {
        "attributes": [
            {
                "name": "accountId",
                "operator": "stringEquals",
                "value": "account-123"
            },
            {
                "key": "serviceName",
                "operator": "stringEquals",
                "value": "cloud-object-storage"
            },
            {
                "key": "serviceInstance",
                "operator": "stringEquals",
                "value": "cd329d97-c33d-4428-b39e-6170dc1c2a1e"
            },
            {
                "key": "resource",
                "operator": "stringMatch",
                "value": "dev-bucket-*"
            },
            {
                "key": "resourceType",
                "operator": "stringEquals",
                "value": "bucket"
            }
        ]
    },
    "rule": {
        "operator": "and",
        "conditions": [
            {
                "key": "{{resource.attributes.path}}",
                "operator": "stringExists",
                "value": true
            },
            {
                "key": "{{resource.attributes.prefix}}",
                "operator": "stringExists",
                "value": false
            },
            {
                "key": "{{resource.attributes.delimiter}}",
                "operator": "stringExists",
                "value": false
            }
        ]
    }
}
```
{: codeblock}
