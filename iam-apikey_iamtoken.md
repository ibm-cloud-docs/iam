---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-20"

keywords: IAM token, token, API key, generate token, access token, temporary credential

subcollection: iam


---

{{site.data.keyword.attribute-definition-list}}

# Generating an {{site.data.keyword.cloud_notm}} IAM token by using an API key
{: #iamtoken_from_apikey}

Generate an {{site.data.keyword.Bluemix}} Identity and Access Management (IAM) token by using either your IAM API key or a service ID's API key. {{site.data.keyword.cloud_notm}} APIs can be accessed only by users who are authorized by an assigned IAM role. Each user who is calling the API must pass credentials for the API to authenticate.
{: shortdesc}

## Generating an IAM token
{: #iamtoken}
{: help}
{: support}

You can generate an IAM token by using either your [{{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey#userapikey) or a [service ID's API key](/docs/account?topic=account-serviceidapikeys). The API key is a permanent credential that can be reused if you don't lose the API key value or delete the API key in the account. This process is also used if you are developing an application that needs to work with other {{site.data.keyword.cloud_notm}} services. You must use a service ID API key to get an access token to be passed to each of the {{site.data.keyword.cloud_notm}} services.

An access token is a temporary credential that expires after 1 hour at the latest. After the acquired token expires, you must generate a new token to continue calling {{site.data.keyword.cloud_notm}} or service APIs, and you can perform only actions that are allowed by your level of assigned access within all accounts. Use the response property `expires_in` in the API response to identify the length of time that your specific access token is valid.
{: note}

## Generate an IAM token by using an API key 
{: #iamtoken-from-apikey-api}

To programmatically generate an IAM token by using an API key, call the [IAM Identity Services API](https://cloud.ibm.com/apidocs/iam-identity-token-api#create-api-key){: external} or [SDKs](https://github.com/IBM/ibm-cloud-sdk-common/blob/main/README.md#authentication){: external} as shown in the following sample request. 

```bash
curl -X POST 'https://iam.cloud.ibm.com/identity/token' -H 'Content-Type: application/x-www-form-urlencoded' -d 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=MY_APIKEY'

```
{: codeblock}
{: curl}

```java
import com.ibm.cloud.sdk.core.security.IamAuthenticator;
import <sdk_base_package>.ExampleService.v1.ExampleService;
...
// Create the authenticator.
IamAuthenticator authenticator = new IamAuthenticator.Builder()
    .apikey("myapikey")
    .build();

// Create the service instance.
ExampleService service = new ExampleService(authenticator);

// 'service' can now be used to invoke operations.
```
{: codeblock}
{: java}

```javascript
const ExampleServiceV1 = require('mysdk/example-service/v1');
const { IamAuthenticator } = require('mysdk/auth');

const authenticator = new IamAuthenticator({
  apikey: '<iam-api-key>',
});

const myService = new ExampleServiceV1({
  authenticator,
});
```
{: codeblock}
{: javascript}

```python
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from <sdk-package-name>.example_service_v1 import *

# Create the authenticator.
authenticator = IAMAuthenticator('myapikey')

# Construct the service instance.
service = ExampleServiceV1(authenticator=authenticator)

# Use 'service' to invoke operations.
```
{: codeblock}
{: python}

```go
import {
    "github.com/IBM/go-sdk-core/v5/core"
    "<appropriate-git-repo-url>/exampleservicev1"
}
...
// Create the authenticator.
authenticator := &core.IamAuthenticator{
    ApiKey: "myapikey",
}

// Create the service options struct.
options := &exampleservicev1.ExampleServiceV1Options{
    Authenticator: authenticator,
}

// Construct the service instance.
service := exampleservicev1.NewExampleServiceV1(options)

// 'service' can now be used to invoke operations.
```
{: codeblock}
{: go}

### Expected response 
{: #response-curl}

```bash
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "not_supported",
  "ims_user_id": 118...90,
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353,
  "scope": "ibm openid"
}
```
{: codeblock}

For more information, see the [IAM Identity Services API](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey). 
{: curl}

For more information, see the [Java SDK](https://github.com/IBM/java-sdk-core/blob/main/Authentication.md){: external}. 
{: java}

For more information, see the [SDK](https://github.com/IBM/ibm-cloud-sdk-common/blob/main/README.md#authentication){: external}. 
{: javascript}

For more information, see the [Python SDK](https://github.com/IBM/python-sdk-core/blob/main/Authentication.md){: external}. 
{: python}

For more information, see the [Go SDK](https://github.com/IBM/go-sdk-core/blob/main/Authentication.md){: external}. 
{: go}

An IAM token is valid for up to 60 minutes, and it is subject to change. When a token expires, you must generate a new one. Use the property `expires_in` for the expiration of the IAM token that you have just created.
{: note}
