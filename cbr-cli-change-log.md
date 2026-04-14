---

copyright:

  years: 2024, 2026
lastupdated: "2026-03-20"

keywords: change log for CBR, updates to CBR, cli, context-based restrictions

subcollection: iam

---

{{site.data.keyword.attribute-definition-list}}

# Context-based restrictions CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the context-based restrictions CLI.

## Version 1.9.0
{: #cli-190}

Version 1.9.0 of the CLI was released on 24 Apr 2025.

Added the **`ibmcloud cbr services`** command, allowing listing of services that CBR rules can be created for.
Added the **`ibmcloud cbr service`** command, allowing querying of details of a particular CBR enabled service.
Added the **`ibmcloud cbr rule-options`** commands, allowing listing of options available for creating a rule against a particular service.
Created grouping for command listing for better visibility.
Added aliases to **`ibmcloud cbr srts`** and **`ibmcloud cbr srt`** for the **`ibmcloud cbr service-ref-targets`** and **`ibmcloud cbr service-ref-target`** commands respectively.
Deprecated the **`ibmcloud cbr api-types`** command.

## Version 1.8.0
{: #cli-180}

Version 1.8.0 of the CLI was released on 25 Sep 2024.

Added **`ibmcloud cbr zone-patch`** and **`ibmcloud cbr rule-patch`** commands, allowing for partial updates instead of full replacements.

## Version 1.7.2
{: #cli-172}

Version 1.7.2 of the CLI was released on 23 Aug 2024.

- Updated the outputs of most commands to be more useful and readable
- Added a mention of implicit global location

## Version 1.7.1
{: #cli-171}

Version 1.7.1 of the CLI was released on 24 Mar 2024.

Updated plugin with compatibility fixes for alpine linux.

## Version 1.7.0
{: #cli-170}

Version 1.7.0 of the CLI was released on 20 Mar 2024.

Added the **`ibmcloud cbr service-ref-target`** command to get information about a specific service reference.

## Version 1.6.0
{: #cli-160}

Version 1.6.0 of the CLI was released on 23 Feb 2024.

- Added enforcement_mode to the output of the **`ibmcloud cbr api-types`** command
- Added `--empty-address-list` flag to the **`ibmcloud cbr zone-create`** and **`ibmcloud cbr zone-udpate`** commands
- Added `--empty-context-list` flag to the **`ibmcloud cbr rule-create`** and **`ibmcloud cbr rule-udpate`** commands

## Version 1.4.1
{: #cli-141}

Version 1.4.1 of the CLI was released on 25 Oct 2023.

- Improved examples
- Added mutual exclusion check for conflicting flags
- Improved error handling and error messages

## Version 1.4.0
{: #cli-140}

Version 1.4.0 of the CLI was released on 21 Sep 2023.

Added `--resource-group` and `--service-group-id` flags to the **`ibmcloud cbr api-types`** command

## Version 1.3.0
{: #cli-130}

Version 1.3.0 of the CLI was released on 30 Jan 2023.

Added private endpoint support for classic infrastructure and VPC infrastructure.

## Version 1.2.0
{: #cli-120}

Version 1.2.0 of the CLI was released on 16 Nov 2022.

- Added `--service-group-id` flag to the following commands: **`ibmcloud cbr rule-create`**,**`ibmcloud cbr rule-update`**, and **`ibmcloud cbr rules`**
- Reordered command args in usage
- Added support for tags
- Improved error catching

## Version 1.1.0
{: #cli-110}

Version 1.1.0 of the CLI was released on 29 Jul 2022.

- Added `--enforcement-mode` flag to the following commands: **`ibmcloud cbr rule-create`**,**`ibmcloud cbr rule-update`**, and **`ibmcloud cbr rules`**

- Added service ref location support to the following commands: **`ibmcloud cbr zone-create`**, **`ibmcloud cbr zone-update`**, and **`ibmcloud cbr service-ref-targets`**

- Added rule API type support to the **`ibmcloud cbr rule-create`** and **`ibmcloud cbr rule-update`** commands

- Added **`ibmcloud cbr api-types`** command for listing available API types

## Context-based restrictions CLI 1.0.0 - 23 Jun 2022
{: #cli-100}

Initial release of the context-based restrictions CLI.
