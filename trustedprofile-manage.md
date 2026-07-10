---

copyright:

  years: 2021, 2026
lastupdated: "2026-07-10"

keywords: trusted profile, federated users, granting access, update trusted profile, compute resource, IAM trusted profile, trust relationship, establish trust,  trust policy, trusted entity, assume access, apply access, remove trusted profile

subcollection: iam

---
{{site.data.keyword.attribute-definition-list}}

# Managing trusted profiles
{: #trusted-profile-update}

Manage trusted profiles by updating the permissions or redefining trust relationships at any time. You can also remove trusted profiles, so compute resources and federated users are unlinked from the profile and can no longer apply the trusted profile identity.
{: shortdesc}

When you remove trusted profiles, you revoke all active sessions. Users are immediately logged out and the removed profiles are no longer available to connect to the target account. API calls that use access tokens might be successful until the access token expires.

You can use {{site.data.keyword.cloudaccesstrailshort}} to monitor which federated users and compute resources apply a trusted profile. For more information, see [Monitoring login sessions for trusted profiles](/docs/iam?topic=iam-trusted-profile-monitor).
{: tip}

## Before you begin
{: #prereqs-manage-tp}

* You must be assigned the administrator, operator, or editor role within the account, or on the IAM Identity Service to manage trusted profiles.

## Updating trusted profiles by using the console
{: #updating-tp-console}
{: ui}

To update trusted profiles, go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select **Trusted profiles**. Then, select the name of the trusted profile that you want to update.

### Updating the description of your profile
{: #description}

Click the name of the trusted profile that you want to update, and select **Actions** > **Edit**. Enter the new name and description, and click **Apply**.

### Improving profile discoverability
{: #profile-discoverability}

When federated users log in, the [profile selection page](/docs/iam?topic=iam-create-trusted-profile#profile-selection-experience) lets them search by profile name, account name, and description, and filter by account or type. How you name and describe your profiles directly affects how quickly users can find the right one.

**Use clear, descriptive names**
:   - Indicate the profile's purpose or role (for example, "Developer - Production Access" or "On-premises owner")
    - Avoid generic names like "Profile 1" or "Test Profile"
    - Keep names concise but meaningful

**Provide detailed descriptions**
:   - Explain what access the profile grants
    - List key actions or resources the profile can access
    - Include any important limitations or restrictions
    - Descriptions are searchable, so include relevant keywords

**Consider multi-account scenarios**
:   - If you manage profiles across multiple accounts, include the account name or business unit in the description
    - Use consistent naming conventions across similar roles in different accounts
    - This helps users quickly identify the right profile when they have access to many accounts

**Optimize for search**
:   - Users can search by profile name, account name, and description
    - Include keywords that users might search for
    - Think about how users will describe the access they need

**Set appropriate session durations**
:   - Choose durations that balance security with user convenience
    - Use shorter durations (1-2 hours) for high-privilege profiles
    - Use longer durations for routine access profiles

By following these practices, you make it easier for users to find the right profile, especially in organizations with many profiles across multiple accounts.

### Redefining the trust relationship
{: #trust}

After the trusted profile is created, you can build trust with both federated users and compute resources in the same trusted profile.

1. Click the name of the trusted profile that you want to update.
2. Click **Add** to add a condition to the existing trust relationship. To edit an existing condition, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit** next to the trust relationship you want to update.
   * Click **Add a condition** and repeat as needed to add more conditions.
   * To remove a condition, click the **Remove** icon ![Remove icon](../icons/close-icon.svg "Remove") next to the existing condition.
3. Click **Save** to apply all added or removed conditions to your trusted profile.

### Assigning access
{: #update-tp-access}

You can assign access to a trusted profile by assigning individual access policies, or by adding the trusted profiles to an existing access group.

#### Assigning access policies
{: #update-tp-policy}

1. Click the name of the trusted profile that you want to update.
2. Click **Access**.
3. To edit existing access policies, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit** next to the access policy you want to update.
4. To assign new access policies, click **Assign**.

You can select your resources based on resource attributes and assign any combination of roles.
{: tip}

#### Assigning access groups
{: #update-tp-group}

1. Click the name of the trusted profile that you want to update.
2. Click **Access**
3. To edit existing access group membership, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Edit** next to the access group you want to update.
4. To add the trusted profile to a new access group, click **Assign group**.
5. Select the access groups to which you want to add the trusted profile and click **Add**. You can assign users to only the access groups that you have access to manage.
6. Click **Assign**.

### Updating session duration
{: #session-duration-tp}

1. Click the name of the trusted profile that you want to update.
2. In the federated users section, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") for the identity provider (IdP) that you want to update.
3. Select **Edit**
4. In hours, enter how long federated users can use this profile before their session expires.
5. Click **Save**.

## Updating trusted profiles by using the CLI
{: #updating-tp-cli}
{: cli}

You can update a trusted profile from your account by using the CLI. For more information, see the [IBM Cloud CLI](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases).

1. Log in, and select the account.

   ```bash
   ibmcloud login
   ```
   {: codeblock}

1. Check the list of trusted profiles for the current account and select the one that you want to update. The following command shows the list of trusted profiles for your {{site.data.keyword.cloud_notm}} account:

   ```bash
   ibmcloud iam trusted-profiles
   ```
   {: codeblock}

1. If you'd like to check the details of a trusted profile, use the `ibmcloud iam trusted-profile` command. Specify the ID or the name of the trusted profile that you would like to check.

   ```bash
   ibmcloud iam trusted-profile <IDorName>
   ```
   {: codeblock}

1. Run the following command to get an overview about the different options.

   ```bash
   ibmcloud iam trusted-profile-update
   ```
   {: codeblock}

1. Update the trusted profile by running the following command. Specify the ID or the name of the trusted profile that you would like to update and rename.

   ```bash
   ibmcloud iam trusted-profile-update <IDorName> -n <NewName> ...
   ```
   {: codeblock}

For example, the following command updates the name `Test trusted profile` to `New test trusted profile`.

   ```bash
   ibmcloud iam trusted-profile-update <Test trusted profile> -n <New test trusted profile> ...
   ```
   {: codeblock}

### Assigning access policies
{: #access-policies-cli}

You can assign new access policies to your trusted profile by using the CLI.

1. Log in, and select the account.

   ```bash
   ibmcloud login
   ```
   {: codeblock}

1. Check the list of trusted profiles for the current account and select the one that you want to assign new access policies to. The following command shows the list of trusted profiles for your {{site.data.keyword.cloud_notm}} account:

   ```bash
   ibmcloud iam trusted-profiles
   ```
   {: codeblock}

1. Assign new access policies by running the following command:

   ```bash
   ibmcloud iam trusted-profile-policy-create
   ```
   {: codeblock}

To check the details of the access policy for a trusted profile, run the following command:

   ```bash
   ibmcloud iam trusted-profile-policy
   ```
   {: codeblock}

For checking the list of access policies for a trusted profile, you can use the `ibmcloud iam trusted-profile-policies` command:

   ```bash
   ibmcloud iam trusted-profile-policies
   ```
   {: codeblock}

You can easily update existing access policies by running the `ibmcloud iam trusted-profile-policy-update` command:

   ```bash
   ibmcloud iam trusted-profile-policy-update
   ```
   {: codeblock}

If you'd like to remove an access policy for a trusted profile, you can use the `ibmcloud iam trusted-profile-policy-delete` command:

   ```bash
   ibmcloud iam trusted-profile-policy-delete
   ```
   {: codeblock}

## Updating trusted profiles by using the API
{: #updating-tp-api}
{: api}

For more information, see the [IAM Identity Services API](/apidocs/iam-identity-token-api).

### Updating the name or description
{: #update-tp-desc-api}

To update the name or description of an existing trusted profile, call the following. Enter your updated `name` and `description` attributes.

   ```bash
   curl -X PUT 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID' -H 'Authorization: Bearer TOKEN' -H 'If-Match: <value of etag header from GET request>' -H 'Content-Type: application/json' -H 'Accept: application/json' -d '{
     "name": "My Profile updated",
     "description": "My updated desc"
   }'
   ```
   {: codeblock}

### Updating the conditions of the trust relationship
{: #trust-api}

After the trusted profile is created, you can build trust with both federated users and compute resources in the same trusted profile.

   ```bash
   curl -X PUT 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID/rules/CLAIM_RULE_ID'
   -H 'Authorization: Bearer TOKEN'
   -H 'If-Match: <value of etag header from GET request>'
   -H 'Content-Type: application/json'
   -H 'Accept: application/json'
   -d '{
      "type": "Profile-SAML",
      "realm_name": "https://w3id.sso.ibm.com/auth/sps/samlidp2/saml20",
      "expiration": 10000,
      "conditions": [
     {
   "claim": "groups",
   "operator": "CONTAINS",
   "value": "\"cloud-docs-ops\""
     }
     ]
   }'
   ```
   {: codeblock}

### Assigning access policies
{: #access-policies-api}

To assign new access policies, call the following:

   ```bash
   curl -X PUT 'https://iam.cloud.ibm.com/v1/policies'
   -H 'Authorization: Bearer $TOKEN'
   -H 'Content-Type: application/json'
   -H 'If-Match: $ETAG'
   -d '{
   "type": "access",
   "description": "Viewer role for for all instances of SERVICE_NAME in the account.",
   "subjects": [
      {
         "attributes": [
         {
            "name": "iam_id",
            "value": "IBMid-123453user"
         }
         ]
      }'
   ],
   "roles":[
      {
         "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
      }
   ],
   "resources":[
      {
         "attributes": [
         {
            "name": "accountId",
            "value": "$ACCOUNT_ID"
         },
         {
            "name": "serviceName",
            "value": "$SERVICE_NAME"
         }
         ]
      }
   ]
   }'
   ```
   {: codeblock}

For more information, see the [IAM Policy Management](/apidocs/iam-policy-management#replace-policy) API.

### Updating session duration
{: #session-duration-tp-api}

To update the session duration for federated users, call the following:

   ```bash
   curl -X PUT 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID/rules/CLAIM_RULE_ID'
   -H 'Authorization: Bearer TOKEN'
   -H 'If-Match: <value of etag header from GET request>'
   -H 'Content-Type: application/json'
   -H 'Accept: application/json'
   -d '{
      "type": "Profile-SAML",
      "realm_name": "https://w3id.sso.ibm.com/auth/sps/samlidp2/saml20",
      "expiration": 10000,
      "conditions": [
     {
   "claim": "groups",
   "operator": "CONTAINS",
   "value": "\"cloud-docs-ops\""
     }
     ]
   }'
   ```
   {: codeblock}

## Removing trusted profiles by using the console
{: #remove-tp-console}
{: ui}

When you remove trusted profiles, compute resources and federated users are unlinked from the profile and can no longer apply the trusted profile identity.
To remove a trusted profile, complete the following steps:

1. To see the full list of trusted profiles in your account, go to **Manage** > **Access (IAM)** in the {{site.data.keyword.cloud_notm}} console, and select **Trusted profiles**.
2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg) next to the trusted profile that you want to remove, and select **Remove**.

## Removing trusted profiles by using the CLI
{: #remove-tp-cli}
{: cli}

You can remove a trusted profile from your account by using the CLI. For more information, see the [IBM Cloud CLI](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases).

1. Log in, and select the account.

   ```bash
   ibmcloud login
   ```
   {: codeblock}

1. Check the list of trusted profiles for the current account and select the one that you want to remove. The following command shows the list of trusted profiles for your {{site.data.keyword.cloud_notm}} account:

   ```bash
   ibmcloud iam trusted-profiles
   ```
   {: codeblock}

1. Remove the trusted profile from your account by running the following command. Specify the ID or the name of the trusted profile that you would like to remove.

   ```bash
   ibmcloud iam trusted-profile-delete <IDorName>
   ```
   {: codeblock}

For example, the following command removes a trusted profile that is named `Test trusted profile`.

   ```bash
   ibmcloud iam trusted-profile-delete <Test trusted profile>
   ```
   {: codeblock}

## Removing trusted profiles by using the API
{: #remove-tp-api}
{: api}

To remove a trusted profile from your account, call the following:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/profiles/PROFILE_ID' -H 'Authorization: Bearer TOKEN'
```
{: codeblock}

For more information, see the [IAM Identity Services API](/apidocs/iam-identity-token-api).
