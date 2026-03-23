---

copyright:

  years: 2018, 2026
lastupdated: "2026-03-23"

keywords: IBM Cloud service APIs, IAM token, API key, authenticate with service API

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Invoking {{site.data.keyword.cloud_notm}} service APIs
{: #iamapikeysforservices}


To authorize applications and services to make API calls, pass your credentials to the service's API to authenticate your user identity and your access to perform actions within the context of the service.
{: shortdesc}

You can identify the caller in one of the following ways:

* {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) token
* {{site.data.keyword.cloud_notm}} API key or service ID API key

[{{site.data.keyword.cloud_notm}} API keys](/docs/account?topic=account-userapikey#manage-user-keys), [service ID API keys](/docs/account?topic=account-serviceidapikeys), and IAM tokens uniquely identify the caller’s identity. The caller identity is either an {{site.data.keyword.cloud_notm}} user or a service ID that was created in an {{site.data.keyword.cloud_notm}} account.

The API keys are credentials that consist of a long series of random characters or numbers. An {{site.data.keyword.cloud_notm}} identity can have multiple API keys. Each of these API keys can be managed independently, meaning if this API key is used by your service only, you can delete the API key without disrupting some other component.

You can use API keys to [log in to the {{site.data.keyword.cloud_notm}} command-line interface (CLI)](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) or to [generate IAM tokens](/docs/iam?topic=iam-iamtoken_from_apikey). While it is not recommended for production use, you can also send API keys to {{site.data.keyword.cloud_notm}} services.

## Passing an {{site.data.keyword.cloud_notm}} IAM token to authenticate with a service's API
{: #token_auth}

To retrieve an IAM access token, the API client must first invoke an {{site.data.keyword.cloud_notm}} IAM API to authenticate and retrieve that token. The preferred way for {{site.data.keyword.cloud_notm}} service API clients is to use an {{site.data.keyword.cloud_notm}} API key to get an IAM access token. The IAM access token, which was implemented as a [JSON Web Token](https://www.ibm.com/think/topics/json-web-tokens){: external}, can be used for multiple invocations of {{site.data.keyword.cloud_notm}} services that accept IAM access tokens as an authentication method. As IAM access tokens are digitally signed with asymmetric keys, {{site.data.keyword.cloud_notm}} services can validate an IAM access token without invoking any external service. This dramatically improves the performance of invoking an API.

![Authenticating with a service API by using an access token](images/tokenauth.svg "Retrieving a token from IAM by using an API key and passing the access token to target services to validate credentials"){: caption="Retrieving a token from IAM by using an API key and passing the access token to target services to validate credentials" caption-side="bottom"}

To authenticate with a service's API by using an access token, complete the following steps:

1. First, [create an {{site.data.keyword.cloud_notm}} API key](/docs/iam?topic=iam-userapikey#manage-user-keys) if you have not already.
2. The next step for the API client is the retrieval of an IAM access token, as described in [Getting an IAM token from an API key](/docs/iam?topic=iam-iamtoken_from_apikey).
3. From the response, extract the property `access_token` to get the IAM access token. `expires_in` indicates the seconds until the IAM access token `access_token` expires. Either use this relative value or the absolute time stamp `expiration` based in [UNIX time](https://en.wikipedia.org/wiki/Unix_time){: external}.
4. Send the IAM access token as described in [RFC 6750, section 2.1. Authorization Request Header Field](https://datatracker.ietf.org/doc/html/rfc6750#page-5){: external}.


Review the following example:
1. Use the HTTP header Authorization
2. Prefix the IAM access token with the literal `Bearer eyJhbGciOiJSUzI1Ng...`
3. Add the prefixed IAM access token to the HTTP header: `Authorization: Bearer eyJhbGciOiJSUzI1Ng...`

```bash
curl -H "Authorization: Bearer eyJhbGciOiJSUzI1Ng..."
```
{: codeblock}
{: curl}

```java
import com.ibm.cloud.sdk.core.security.BearerTokenAuthenticator;
import <sdk_base_package>.ExampleService.v1.ExampleService;
...
String bearerToken = // ... obtain bearer token value ...

// Create the authenticator.
BearerTokenAuthenticator authenticator = new BearerTokenAuthenticator(bearerToken);

// Create the service instance.
ExampleService service = new ExampleService(authenticator);

// 'service' can now be used to invoke operations.
...
// Later, if your bearer token value expires, you can set a new one like this:
newToken = // ... obtain new bearer token value
authenticator.setBearerToken(newToken);
```
{: codeblock}
{: java}

```javascript
const ExampleServiceV1 = require('mysdk/example-service/v1');
const { BearerTokenAuthenticator } = require('mysdk/auth');

const authenticator = new BearerTokenAuthenticator({
  bearerToken: '<access-token>',
});

const myService = new ExampleServiceV1({
  authenticator,
});
...

// Later when the access token expires, the application must acquire
// a new access token, then set it on the authenticator.
// Subsequent request invocations will include the new access token.
authenticator.setBearerToken('<new-access-token>')
```
{: codeblock}
{: javascript}

```python
from ibm_cloud_sdk_core.authenticators import BearerTokenAuthenticator

authenticator = BearerTokenAuthenticator(<your_bearer_token>)
service = ExampleService(authenticator=authenticator)

# after getting a new access token...
service.get_authenticator().set_bearer_token('54321');
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
bearerToken := // ... obtain bearer token value ...
authenticator := &core.BearerTokenAuthenticator{
    BearerToken: bearerToken,
}

// Create the service options struct.
options := &exampleservicev1.ExampleServiceV1Options{
    Authenticator: authenticator,
}

// Construct the service instance.
service := exampleservicev1.NewExampleServiceV1(options)

// 'service' can now be used to invoke operations.
...
// Later, if your bearer token value expires, you can set a new one like this:
newToken := // ... obtain new bearer token value
authenticator.BearerToken = newToken
```
{: codeblock}
{: go}

Use the same IAM access token for subsequent IBM Cloud service API calls to achieve the best performance and scalability.
{: tip}

[Java SDK reference](https://github.com/IBM/java-sdk-core/blob/main/Authentication.md#bearer-token-authentication){: external}
{: java}

[Node SDK reference](https://github.com/IBM/ibm-cloud-sdk-common/blob/main/README.md#3-create-a-bearer-token-authenticator-programmatically)
{: javascript}

[Python SDK reference](https://github.com/IBM/ibm-cloud-sdk-common/blob/main/README.md#3-create-a-bearer-token-authenticator-programmatically)
{: python}

[Go SDK reference](https://github.com/IBM/go-sdk-core/blob/main/Authentication.md#bearer-token-authentication)
{: go}


## Passing an {{site.data.keyword.cloud_notm}} API key to authenticate with a service API
{: #apikey_auth}

API clients can directly pass an {{site.data.keyword.cloud_notm}} API key to the target service’s API. To do so, send the `apikey` keyword as the user name and the {{site.data.keyword.cloud_notm}} API key as the password by using basic authorization HTTP header to the target service.

It is recommended that in all cases of passing an API key to a service API that you use an API key for a service ID or a user API key that is associated with a functional ID that is assigned only the level of access required to work with the particular service.
{: tip}

The target service API must introspect the {{site.data.keyword.cloud_notm}} API key by using the {{site.data.keyword.cloud_notm}} IAM service. The following graphic shows three API interactions. The {{site.data.keyword.cloud_notm}} API key is passed to every target service’s API, so each target service must look up the {{site.data.keyword.cloud_notm}} API key details by invoking {{site.data.keyword.cloud_notm}} IAM.

![Authenticating with a service API by using an API key](images/APIkeyauth.svg "Passing API keys to target services which then pass the API key to IAM to validate credentials"){: caption="Passing API keys to target services which then pass the API key to IAM to validate credentials" caption-side="bottom"}

Using an {{site.data.keyword.cloud_notm}} API key is convenient, and it makes it easy to discover new APIs and quickly try out prototypes. This method requires you to send the {{site.data.keyword.cloud_notm}} API key to the target service‘s API in a readable format, which unnecessarily compromises the API key. Additionally, as the target service’s API must always introspect the API key, this method is less performant and therefore not recommended for production work loads.

To authenticate with a service's API by using an API key, complete the following steps:

1. First, [create an {{site.data.keyword.cloud_notm}} API key](/docs/account?topic=account-userapikey#manage-user-keys) if you have not already.
2. Send the {{site.data.keyword.cloud_notm}} API key as defined in [RFC 7617](https://datatracker.ietf.org/doc/html/rfc7617){: external} as HTTP header “Authorization”. Use `apikey` as the user name, and the API key value as the password.


As an example, the following steps assume that the API key is 0a1A2b3B4c5C6d7D8e9E:

1. Concatenate the user name `apikey` and the API key that is separated by a colon: `apikey:0a1A2b3B4c5C6d7D8e9E`
2. Base64 encode the string: `base64("apikey:0a1A2b3B4c5C6d7D8e9E") => YXBpa2V5OjBhMUEyYjNCNGM1QzZkN0Q4ZTlF`
3. Set the HTTP header Authorization with schema Basic, for example `Authorization: Basic YXBpa2V5OjBhMUEyYjNCNGM1QzZkN0Q4ZTlF`. When you use the curl command, you can pass this with the parameter -u:

```bash
curl -u "apikey:<IBM Cloud API key value>"
```
{: codeblock}
{: curl}

```java
import com.ibm.cloud.sdk.core.security.BasicAuthenticator;
import <sdk_base_package>.ExampleService.v1.ExampleService;
...
// Create the authenticator.
BasicAuthenticator authenticator = new BasicAuthenticator.Builder()
    .username("myuser")
    .password("mypassword")
    .build();

// Create the service instance.
ExampleService service = new ExampleService(authenticator);

// 'service' can now be used to invoke operations.
```
{: codeblock}
{: java}

```javascript

```
{: codeblock}
{: javascript}

```python
from ibm_cloud_sdk_core.authenticators import BasicAuthenticator

authenticator = BasicAuthenticator(<your_username>, <your_password>)
service = ExampleService(authenticator=authenticator)
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
authenticator := &core.BasicAuthenticator{
    Username: "myuser",
    Password: "mypassword",
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

The username is `apikey` and the password is the api key itself.
