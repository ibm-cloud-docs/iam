---

copyright:

  years: 2019, 2026
lastupdated: "2026-03-31"

keywords: access, users, service IDs, access group, IAM, policy, characters, wildcard, operators, asterisk, question mark, *, ?, JSON document, policy document

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Assigning access by using wildcard policies
{: #wildcard}

When you're assigning access to certain IAM-enabled services, you can use advanced operators in a [policy](#x2853407){: term} to grant access to resources that satisfy specific naming conventions. By using wildcard policies, you can reduce the number of policies that are required for managing access to some resources.
{: shortdesc}

To assign access, you need the administrator role on the resource. For more information, see [IAM access](/docs/iam?topic=iam-userroles).

## JSON policy document
{: #policy-js}

Most access policies are stored in {{site.data.keyword.cloud}} as JSON documents. When you use the `stringEquals` operator in a policy, an exact string match is performed between the query and the target string. When you use the `stringMatch` operator, a case-sensitive string match is performed between the pattern and the target string using either an asterisk (`*`), question mark (`?`), both, or literal values. An asterisk (`*`) represents any sequence of zero or more characters in the string, and a question mark (`?`) represents any single character. See the following examples:

* `*dev*` matches any string that contains `dev`
* `dev*` matches any string that begins with `dev`
* `*dev` matches any string that ends with `dev`

Refer to the documentation for the specific service that you are assigning access to for details about the supported operators for specific attributes for that service.
{: note}

### Using an asterisk (`*`) as a wildcard
{: #policy-doc-asterisk}

The following example shows how you might create a policy that gives a user access to manage all {{site.data.keyword.messagehub}} topics that start with `dev` in a particular account.

```bash
{
    "type": "access",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "iam_id",
                    "value": "IBMid-12345"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "d727f71e99b14534b3267fab8cc9b09a"
                },
                {
                    "name": "serviceName",
                    "value": "messagehub"
                },
                {
                    "name": "resourceType",
                    "value": "topic"
                },
                {
                    "name": "resource",
                    "operator": "stringMatch",
                    "value": "dev*"
                }
            ]
        }
    ]
}
```
{: codeblock}

### Using a question mark (`?`) as a wildcard
{: #policy-doc-multiwildcards}

The following example shows how you can create a policy that gives a user access to edit any {{site.data.keyword.messagehub}} topic that ends in a particular pattern.

On the line `"value": "*??81"`, the `*` indicates zero or more characters and matches any string that ends with `??81`. The `?` represents a single character. Since there are two `??`, the resulting pattern matches a string of four or more characters that end in `81`.

```bash
{
    "type": "access",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "iam_id",
                    "value": "IBMid-12345"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "d727f71e99b14534b3267fab8cc9b09a"
                },
                {
                    "name": "serviceName",
                    "value": "messagehub"
                },
                {
                    "name": "resourceType",
                    "operator": "stringEquals"
                    "value": "topic",
                },
                {
                    "name": "resource",
                    "operator": "stringMatch",
                    "value": "*??81"
                }
            ]
        }
    ]
}
```
{: codeblock}

### Using an asterisk (`*`) and question mark (`?`) as a literal character
{: #literal}

You can express an asterisk (`*`) and question mark (`?`) as a literal character, ensuring that they aren't interpreted as a wildcard by enclosing each within two sets of curly brackets `{{}}`.

The following example shows how you can create a policy that gives a user access to edit an Event Streams topic that contains the literal characters `*` and `?`. The topic must end with the pattern `.?.log`, implying any single character between the periods `.` followed by the `log` string.

```json
{
    "type": "access",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "iam_id",
                    "value": "IBMid-12345"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "d727f71e99b14534b3267fab8cc9b09a"
                },
                {
                    "name": "serviceName",
                    "value": "messagehub"
                },
                {
                    "name": "resourceType",
                    "operator": "stringEquals"
                    "value": "topic",
                },
                {
                    "name": "resource",
                    "operator": "stringMatch",
                    "value": "dev-topic-{{*}}-{{?}}.?.log"
                }
            ]
        }
    ]
}
```
{: codeblock}
{: pre}

On the line `"value": "dev-topic-{{*}}-{{?}}.?.log"`, the `{{*}}` indicates the character `*` and the `{{?}}` indicates the character `?`. Therefore, a topic such as `dev-topic-*-?.1.log` matches this pattern.

The following two examples represent the same evaluation where a case-sensitive string comparison of `dev*` is performed.

```json
{
    "name": "resource",
    "operator": "stringMatch",
    "value": "dev{{*}}"
}
```
{: codeblock}

```json
{
    "name": "resource",
    "operator": "stringEquals",
    "value": "dev*"
}
```
{: codeblock}

## String comparisons
{: #string-comparisons}

{{_include-segments/string-compare-intro-reuse.md}}

{{_include-segments/string-compare-table-reuse.md}}
