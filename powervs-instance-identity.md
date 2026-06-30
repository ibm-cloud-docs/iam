---

copyright:

  years: 2026, 2026
lastupdated: "2026-06-30"

keywords: Power Virtual Server, PowerVS, instance identity, metadata service, instance identity token, trusted profile, workload identity, compute resource identity

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Authenticating {{site.data.keyword.powerSys_notm}} instances with trusted profiles
{: #powervs-instance-identity}

{{site.data.keyword.powerSys_notm}} instances can use instance identity tokens to authenticate with {{site.data.keyword.cloud}} services through trusted profiles, eliminating the need to store and manage API keys. The instance metadata service provides JSON Web Tokens (JWT) containing instance claims. IAM validates these claims against trusted profile conditions to grant access.
{: shortdesc}

## Acquiring an instance identity token
{: #powervs-acquire-token}

Applications running on a {{site.data.keyword.powerSys_notm}} instance can acquire an instance identity token from the instance metadata service.

To acquire an instance identity token, make an HTTP PUT request to the {{site.data.keyword.powerSys_notm}} metadata service endpoint from within your instance:

```bash
curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" \
  -H "Metadata-Flavor: ibm" \
  -H "Content-Type: application/json" \
  -d '{ }'
```
{: codeblock}

You can optionally specify a custom expiration time in seconds for the token by including an `expires_in` parameter in the request body. The default expiration is 300 seconds or 5 minutes.

```bash
curl -X PUT "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/token" \
  -H "Metadata-Flavor: ibm" \
  -H "Content-Type: application/json" \
  -d '{ "expires_in": 600 }'
```
{: codeblock}

The response contains a JSON object with the instance identity token:

```json
{
    "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Il...",
    "created_at": "2026-05-27T15:45:31Z",
    "expires_at": "2026-05-27T15:50:31Z",
    "expires_in": 300
}
```
{: codeblock}

## Instance identity token structure
{: #powervs-token-structure}

The instance identity token is a JWT that contains the following types of claims:

Standard JWT claims
:   Standard claims such as `iss` (issuer), `aud` (audience), `exp` (expiration time), `nbf` (not before time), and `iat` (issued at time).

{{site.data.keyword.powerSys_notm}} instance claims
:   Claims that identify the specific {{site.data.keyword.powerSys_notm}} instance and its attributes:
    * `workspaces` - Array of workspace objects containing name and CRN
    * `subnets` - Array of subnet objects containing name and CRN
    * `iaas.crn` - Instance CRN
    * `iaas.name` - Instance name
    * `iaas.account_id` - Account ID of the instance
    * `iaas.zone` - Zone where the instance is located
    * `iaas.region` - Region where the instance is located
    * `iaas.resource_group_id` - Resource group ID

Example token claims:

```json
{
  "workspaces": [
    {
      "name": "Dal12 Workspace",
      "crn": "crn:v1:staging:public:power-iaas:dal12:a/003a57244a924fa4a579cacb83ddcc65:2ba780b5-3e13-4079-941d-462412a8c56c::"
    }
  ],
  "subnets": [
    {
      "name": "public-192_168_192_56-29-VLAN_2003",
      "crn": "crn:v1:staging:public:power-iaas:dal12:a/003a57244a924fa4a579cacb83ddcc65:2ba780b5-3e13-4079-941d-462412a8c56c:network:89ace85c-873e-43d1-9b9a-387773533313"
    }
  ],
  "iaas": {
    "crn": "crn:v1:staging:public:power-iaas:dal12:a/003a57244a924fa4a579cacb83ddcc65:2ba780b5-3e13-4079-941d-462412a8c56c:pvm-instance:af3c84d1-4cec-4dc0-9341-26586e45c78f",
    "name": "mds-test-2",
    "account_id": "003a57244a924fa4a579cacb83ddcc65",
    "zone": "dal12",
    "region": "us-south",
    "resource_group_id": "f31b872a96c34479ae0c59b2e7555319",
    "satellite_location": ""
  },
  "iss": "PVS-CR_us-south",
  "aud": [
    "PVS-CR_us-south",
    "1234"
  ],
  "exp": 1779897031,
  "nbf": 1779896731,
  "iat": 1779896731
}
```
{: codeblock}

## Creating conditions for trusted profiles
{: #powervs-token-conditions}

When creating trusted profile conditions to match {{site.data.keyword.powerSys_notm}} instances, it's important to understand how to work with array fields like `workspaces` and `subnets`.

### Working with array fields
{: #powervs-array-fields}

The `workspaces` and `subnets` claims are arrays of objects.
When using the `CONTAINS` operator with these array fields, IAM checks if the exact value you provide matches any element in the array using the `EQUALS` comparator. The `CONTAINS` operator works differently depending on the attribute type:

- For arrays like `workspaces` and `subnets`: Checks if the provided value exactly matches any element in the array
- For strings like `iaas.name` and `iaas.region`: Checks if the provided value is contained within the string

For example, when matching a subnet by name:

- `subnets.name CONTAINS "FVT-NG-Netw-Subnet"` matches if any subnet in the array has exactly this name
- `subnets.name CONTAINS "FVT-NG-Netw"` does not match because `CONTAINS` checks for exact matches in arrays, not substring matches

### Example conditions
{: #powervs-example-conditions}

The following examples show how to use condition attributes to match Power Virtual Server instances.

To match instances in a specific workspace:
```
workspaces.name EQUALS "Dal12 Workspace"
```

To match instances connected to a specific subnet:
```
subnets.name CONTAINS "public-192_168_192_56-29-VLAN_2003"
```

To match instances in a specific region:
```
iaas.region EQUALS "us-south"
```

To match instances with a name containing a pattern:
```
iaas.name CONTAINS "production"
```

For more information about condition operators, see [IAM condition properties](/docs/iam?topic=iam-iam-condition-properties).

## Using instance identity tokens with trusted profiles
{: #powervs-token-trusted-profiles}

After acquiring an instance identity token, your application can exchange it for an IAM access token through the {{site.data.keyword.powerSys_notm}} metadata service. The exchange must be done from within the VM using the metadata service endpoint.

To exchange the instance identity token for an IAM access token, make a request to the metadata service with your trusted profile information:

```bash
curl -X POST "https://api.metadata.power-iaas.cloud.ibm.com/identity/v1/iam_tokens" \
  -H "Content-Type: application/json" \
  -H "Metadata-Flavor: ibm" \
  -H "Authorization: Bearer $INSTANCE_IDENTITY_TOKEN" \
  -d '{
    "trusted_profile": {
      "id": "TRUSTED_PROFILE_ID"
    }
  }'
```
{: codeblock}

You can specify the trusted profile by using one of the following attributes in the `trusted_profile` object:
* `id` - The trusted profile ID
* `crn` - The trusted profile CRN
* `name` - The trusted profile name

IAM validates the instance identity token and checks whether the instance's attributes match the conditions defined in the trusted profile. If the validation succeeds, IAM returns an access token that your application can use to call {{site.data.keyword.cloud_notm}} services.

The instance identity token cannot be exchanged directly through the [IAM API](https://iam.cloud.ibm.com/identity/token){: external}. Token exchange must be performed through the {{site.data.keyword.powerSys_notm}} metadata service endpoint from within the VM.
{: important}

## Token validation
{: #powervs-token-validation}

When you use an instance identity token to assume a trusted profile, IAM performs the following validation steps:

1. Verifies that the token signature is using the public key from the {{site.data.keyword.powerSys_notm}} metadata service.
2. Checks that the token has not expired.
3. Validates that the token's claims match the conditions defined in the trusted profile.
4. Confirms that the instance belongs to the account where the trusted profile is defined.

If all validation steps succeed, IAM issues an access token with the permissions assigned to the trusted profile.

## Security considerations
{: #powervs-security-considerations}

When using {{site.data.keyword.powerSys_notm}} instance identity tokens with trusted profiles, consider the following security best practices:

* Instance identity tokens are scoped to the specific instance and cannot be used from other instances
* Tokens have a limited lifetime and must be refreshed periodically
* Use specific conditions in your trusted profiles to limit which instances can assume the profile
* Monitor trusted profile usage using {{site.data.keyword.cloudaccesstrailshort}}
* Follow the principle of least privilege when assigning permissions to trusted profiles
