---
title: What's new in version 2207
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2207 of Configuration Manager current branch.
ms.date: 08/01/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: paasin
ms.author: paasin
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: highpri
---

# What's new in version 2207 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2207 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2103 or later. <!-- baseline only statement: When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update.--> This article summarizes the changes and new features in Configuration Manager, version 2207.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2207](../../servers/manage/checklist-for-installing-update-2207.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2207.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Cloud-attached management

### Administration Service Management option
<!--12952905-->
When configuring Azure Services, a new option called **Administration Service Management** is now added for enhanced security. Selecting this option allows administrators to segment their admin privileges between cloud management gateway (CMG) and administration service. By enabling this option, access is restricted to only administration service endpoints. Configuration Management clients will authenticate to the site using Azure Active Directory.
 
For more information, see [Configure Azure services for use with Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

### Improvements to cloud management gateway (CMG) workflow
<!--13351390#-->

You can now approve the application workflow through email. For the application approvals through email, manually add the CMG URL in the Azure Active Directory app as single page application redirect URI. 

<!--For more information, see [xxxxxc](../../servers/blah.md). -->

## Site infrastructure

### Microsoft Defender for Endpoint onboarding for Windows Server 2012 R2 and Windows Server 2016
<!--9265511-->
Configuration Manager will now utilize the Windows Server 2012 R2 and Windows Server 2016 unified solution for anti-virus and endpoint detection and response. Devices that are targeted with Microsoft Defender for Endpoint onboarding policy will use the unified agent versus the previous Microsoft Monitoring Agent based solution (where applicable).

<!--For more information, see [xxxxxc](../../servers/blah.md). -->


### Default site boundary group behavior to support cloud source selection
<!--10674394-->
You can now add options via PowerShell to include and prefer cloud management gateway (CMG) management points for the default site boundary group. When a site is set up, there's a default site boundary group created for each site and all the clients are by default mapped to it until they're assigned to some custom boundary group.

<!--For more information, see [xxxxxc](../../servers/blah.md). -->

## Client management

### Script execution timeout for compliance settings
<!--14120481-->
You can now define a **Script Execution Timeout (seconds)** when configuring client settings for compliance settings. The timeout value can be set from a minimum of 60 seconds to a maximum of 600 seconds. This new setting allows you more flexibility for configuration items when you need to run scripts that may exceed the default of 60 seconds.

<!--For more information, see [xxxxxc](../../servers/blah.md). -->

## Collections



<!-- ## Software Center -->

## Software updates

### Folders for automatic deployment rules (ADRs)
<!--13507410-->

Admins can now organize ADRs by using folders. This change allows for better categorization and management of ADRs. Folder management for ADRs is also supported with PowerShell cmdlets.

<!--For more information, see [xxxxxc](../../servers/blah.md). -->

### Offset for reoccuring monthly maintenance window schedules
<!--3601127#-->

Based upon your feedback, you can now offset monthly maintenance window schedules to better align deployments with the release of monthly security updates. For example, using an offset of two days after the second Tuesday of the month, sets the maintenance window for Thursday.

<!--For more information, see [xxxxxc](../../servers/blah.md). -->

## OS deployment





<!--## Protection-->

## Application management



## Community hub



## Configuration Manager console






<!--## Tools-->

<!--## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.



As previously announced, version 2207 drops support for the following features:
-->

## Other updates

<!--Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):
-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2207 release notes](/powershell/sccm/2207-release-notes).

<!--

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2111/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2111 | May 11, 2021 | No |
-->

## Next steps


At this time, version 2207 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2207.md#early-update-ring).


<!--As of April 26, 2022, version 2207 is globally available for all customers to install.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2207](../../servers/manage/checklist-for-installing-update-2207.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2207.md#post-update-checklist).
