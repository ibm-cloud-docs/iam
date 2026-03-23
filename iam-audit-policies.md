---

copyright:

  years: 2021, 2026
lastupdated: "2026-03-23"

keywords: auditing IAM policies, last permit information, restore policies, inactive policies

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Auditing access policies
{: #iam-audit-policies}

To reduce the number of policies in the account and keep only the minimum access that is necessary for each user, you can identify the infrequently used access policies. You can determine whether to remove them, or in some cases, you might expect an infrequently used policy.
{: shortdesc}

Access policies are how users, service IDs, access groups, and trusted profiles in the account are given permission to access and take actions on account resources. Policies include a subject, target, and role. The subject is the user, service ID, or access group that you are providing access. The target of the policy is the resource to which you want to provide access. And, the {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) roles define the level of access or allowed actions on the target of the policy. In addition to access policies for users and service IDs, there is a policy type that is called an authorization that allows specific services or instances of services access to other services. You can learn more about assigning access between services in the [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth) documentation. For more information about access policies, see [What are IAM policies and who can assign them?](/docs/account?topic=account-iamusermanpol).

IAM captures authorization information for each policy. This information includes the last time that the policy was used to grant a permit and a running count of its use.

## Managing inactive policies in the console
{: #iam-audit-policies-list}
{: ui}

The inactive policies report shows policies that haven't permitted access in the last 30 days or longer. Policies that have never permitted access are not included.

To view inactive policies, you need the Editor role or higher on the AM Insight service, the IAM Access Management service, or on All Account Management services.

To manage inactive policies in the console, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Inactive policies**.
1. Determine whether you can remove the inactive policies in the report.
1. To delete inactive policies, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Remove**.

When you delete a policy, it's no longer included for authorization evaluations. IAM keeps a copy of all deleted policies for 10 days. During this time period, you can list and restore them at any time. To restore a deleted policy, see [Restoring deleted policies by using the API](/docs/iam?topic=iam-iam-audit-policies&interface=api#iam-audit-policies-restore).
{: note}

## Exporting user access policy reports
{: #audit-user-access-policies}
{: ui}

You can export an access policy report for each user in your account if you are the account owner, have the Editor role or higher on the User Management service, or have the Editor role or higher on the IAM Access Management service. The access policy report lists all of the access policies that the user has, including the policies that are associated with access groups that the user is a member of.

Auditing user's access policies ensures that you're using the principle of least privilege. Use the report to determine whether the user is assigned to the appropriate access policies, and take the needed action to reduce the number of access policies.

To export the report, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access(IAM)**, and select **Users**.
1. Determine the user that you want to audit and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg) > **Access report**.
1. Click **Download JSON** or **Download CSV**.

## Listing policies with last permit information by using the API
{: #iam-audit-policies-list-api}
{: api}

List all account policies including last permit information that is sorted by count or last used. The policy metadata can be retrieved by using the [IAM Policy Management API](/apidocs/iam-policy-management#policy-data-enrichment).

```curl
curl -X GET https://iam.cloud.ibm.com/v1/policies?account_id=<>&format=include_last_permit&sort=-last_modified_at \
  -H 'Authorization: Bearer $TOKEN' \
  -H 'Content-Type: application/json'
```
{: codeblock}
{: curl}

```java
ListPoliciesOptions options = new ListPoliciesOptions.Builder()
    .accountId(exampleAccountId)
    .iamId(exampleUserId)
    .format("include_last_permit")
    .build();

Response<PolicyList> response = service.listPolicies(options).execute();
PolicyList policyList = response.getResult();

System.out.println(policyList);
```
{: codeblock}
{: java}

```javascript
const params = {
  accountId: exampleAccountId,
  iamId: exampleUserId,
  format: 'include_last_permit',
};

iamPolicyManagementService.listPolicies(params)
  .then(res => {
    console.log('listPolicies() result:\n' + JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: codeblock}
{: javascript}

```python
policy_list = iam_policy_management_service.list_policies(
  account_id=example_account_id, iam_id=example_user_id, format='include_last_permit'
).get_result()

print(json.dumps(policy_list, indent=2))
```
{: codeblock}
{: python}

```go
options := iamPolicyManagementService.NewListPoliciesOptions(
  exampleAccountID,
)
options.SetIamID(exampleUserID)
options.SetFormat("include_last_permit")

policyList, response, err := iamPolicyManagementService.ListPolicies(options)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(policyList, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}

* `format=include_last_permit`: Include the last permit information for each policy.
* `sort=last_permit_at`: Sort by date in ascending order. The policies that have not been used for any permits and the oldest permits are listed first.

The format of the response is represented in JSON.

```json
{
    "policies": [
        {
            "id": "45b226ac-490d-47f3-a785-990e0c729d93",
            "type": "access",
            "subjects": [...],
            "roles": [...],
            "resources": [...],
            ...
            "last_modified_at": "2021-04-09T14:36:30.505Z",
            "last_modified_by_id": "IBMid-310000JVN5",
            "last_permit_at": null,       <-- IAM has no record of this policy ever granting a permit decision. This will be reset when this policy is deleted.
          "last_permit_frequency": 0,
            "state": "active"
        },
        {
            "id": "11155157-afb3-4792-9ebd-b1f5547be224",
            "type": "access",
            "subjects": [...],
            "roles": [...],
            "resources": [...],
            ...
            "last_modified_at": "2019-05-09T15:28:07.045Z",
            "last_modified_by_id": "IAM",
            "last_permit_at": "2021-04-20T19:45:44.058Z",
            "last_permit_frequency": 137,  <-- it has been used this many times since IAM started keeping track
            "state": "active"
        },
...
```
{: codeblock}

## Deleting unused policies by using the API
{: #iam-audit-policies-delete}
{: api}

You identified one or more policies that have not been used to grant access in a while. You can delete the unused policies as shown in the following examples.

```curl
curl -X DELETE https://iam.cloud.ibm.com/v1/policies/{examplePolicyId} \
    -H 'Authorization: Bearer $TOKEN'
```
{: codeblock}
{: curl}

```java
DeletePolicyOptions options = new DeletePolicyOptions.Builder()
    .policyId(examplePolicyId)
    .build();

service.deletePolicy(options).execute();
```
{: codeblock}
{: java}

```javascript
const params = {
  policyId: examplePolicyId,
};

iamPolicyManagementService.deletePolicy(params)
  .then(res => {
    console.log('deletePolicy() response status code: ' + res.status);
  })
  .catch(err => {
    console.warn(err)
  });
```
{: codeblock}
{: javascript}

```python
response = iam_policy_management_service.delete_policy(
  policy_id=example_policy_id
).get_result()

print(json.dumps(response, indent=2))
```
{: codeblock}
{: python}

```go
options := iamPolicyManagementService.NewDeletePolicyOptions(
  examplePolicyID,
)

response, err := iamPolicyManagementService.DeletePolicy(options)
if err != nil {
  panic(err)
}
```
{: codeblock}
{: go}

For more information, see [Delete a policy by ID](/apidocs/iam-policy-management#delete-policy).

The policy is deleted and no longer included for authorization evaluations. IAM keeps a copy of all deleted policies for 10 days.
{: note}

## Restoring deleted policies by using the API
{: #iam-audit-policies-restore}
{: api}

You found out that a policy that was recently deleted is needed. In that case, you can follow these steps to restore the policies.

1. List deleted policies in the account and sort by the last modified time.

    ```curl
    curl -X GET https://iam.cloud.ibm.com/v1/policies?account_id=<>&state=deleted&sort=last_modified_at \
      -H 'Authorization: Bearer $TOKEN' \
      -H 'Content-Type: application/json'
    ```
    {: codeblock}
    {: curl}

    ```java
    ListPoliciesOptions options = new ListPoliciesOptions.Builder()
          .accountId(exampleAccountId)
          .iamId(exampleUserId)
          .state("deleted")
          .sort("last_modified_at")
          .build();

    Response<PolicyList> response = service.listPolicies(options).execute();
    PolicyList policyList = response.getResult();

    System.out.println(policyList);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      accountId: exampleAccountId,
      iamId: exampleUserId,
      sort: 'last_modified_at',
      state: 'deleted'
    };

    iamPolicyManagementService.listPolicies(params)
      .then(res => {
          console.log('listPolicies() result:\n' + JSON.stringify(res.result, null, 2));
      })
      .catch(err => {
          console.warn(err)
      });
    ```
    {: codeblock}
    {: javascript}

    ```python
    policy_list = iam_policy_management_service.list_policies(
      account_id=example_account_id, iam_id=example_user_id, state='deleted', sort='last_modified_at'
    ).get_result()

    print(json.dumps(policy_list, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    options := iamPolicyManagementService.NewListPoliciesOptions(
      exampleAccountID,
    )
    options.SetIamID(exampleUserID)
    options.SetSort("last_modified_at")
    options.SetState("deleted")

    policyList, response, err := iamPolicyManagementService.ListPolicies(options)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(policyList, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

    The format of the response is represented in JSON.

    ```json
    {
        "policies": [
            {
                "id": examplePolicyId1,
                "type": "access",
                "subjects": [...],
                "roles": [...],
                "resources": [...],
                ...
                "last_modified_at": "2021-04-09T14:36:30.505Z",
                "last_modified_by_id": "IBMid-310000JVN5",
                "last_permit_at": null,
                "last_permit_frequency": 0,
                "state": "deleted"  <-- deleted policy
            },
            {
                "id": examplePolicyId2,
                "type": "access",
                "subjects": [...],
                "roles": [...],
                "resources": [...],
                ...
                "last_modified_at": "2019-05-09T15:28:07.045Z",
                "last_modified_by_id": "IAM",
                "last_permit_at": null,
                "last_permit_frequency": 0,
                "state": "deleted"  <-- deleted policy
            },
    ...
    ```
    {: codeblock}

2. With the previously retrieved policy ID, you can restore the policy:

    ```curl
    curl -X PATCH 'https://iam.cloud.ibm.com/v1/policies/{examplePolicyId}' \
      -H 'Authorization: Bearer $TOKEN' \
      -H 'Content-Type: application/json' \
      -H 'If-Match: $ETAG' \
      -d '{"state": "active"}'
    ```
    {: codeblock}
    {: curl}

    ```java
    PatchPolicyOptions patchPolicyOptions = new PatchPolicyOptions.Builder()
            .policyId(examplePolicyId)
            .ifMatch(examplePolicyEtag)
            .state("active")
            .build();

    Response<Policy> response = service.patchPolicy(patchPolicyOptions).execute();
    Policy policy = response.getResult();

    System.out.println(policy);
    ```
    {: codeblock}
    {: java}

    ```javascript
    const params = {
      policyId: examplePolicyId,
      ifMatch: examplePolicyETag,
      state: 'active'
    };

    iamPolicyManagementService.patchPolicy(params)
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
    policy = iam_policy_management_service.patch_policy(
      policy_id=example_policy_id,
      if_match=example_updated_policy_etag,
      state='active'
    ).get_result()

    print(json.dumps(policy, indent=2))
    ```
    {: codeblock}
    {: python}

    ```go
    options := iamPolicyManagementService.NewPatchPolicyOptions(
      examplePolicyID,
      examplePolicyETag,
    )

    options.SetState("active")

    policy, response, err := iamPolicyManagementService.PatchPolicy(options)
    if err != nil {
      panic(err)
    }
    b, _ := json.MarshalIndent(policy, "", "  ")
    fmt.Println(string(b))
    ```
    {: codeblock}
    {: go}

    The format of the response is represented in JSON.

    ```json
    {
        "id": examplePolicyId,
        "type": "access",
        "subjects": [...],
        "roles": [...],
        "resources": [...],
        ...
        "last_modified_at": "2021-04-09T14:36:30.505Z",
        "last_modified_by_id": "IBMid-310000JVN5",
        "last_permit_at": null,
        "last_permit_frequency": 0,
        "state": "active"  <-- policy is active again
    }
    ```
    {: codeblock}

    For more information, see [Restore a deleted policy by ID](/apidocs/iam-policy-management#replace-policy).

## Next steps
{: #audit-policies-next-steps}

Gain insight on the access assignments in your account from different perspectives. View [Auditing access to resources](/docs/account?topic=account-access-report) to learn what identities and services can access a specific resource.
