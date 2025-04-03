---
title: What's new in version 2403
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2403 of Configuration Manager current branch.
ms.date: 04/05/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2403 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2403 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2211 or later. When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability. This article summarizes the changes and new features in Configuration Manager, version 2403.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2403](../../servers/manage/checklist-for-installing-update-2403.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2403.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure

### Microsoft Azure Active Directory rebranded to Microsoft Entra ID

Starting Configuration Manager version 2403, Microsoft Azure Active Directory is renamed to Microsoft Entra ID within Configuration Manager.

For more information, see [New name for Azure Active Directory](/entra/fundamentals/new-name).

### Automated diagnostic Dashboard for Software Update Issues

A new dashboard is added to the console under monitoring workspace, which shows the diagnosis of the software update issues in your environment this feature can easily identify  any issues related to software updates. You can fix software update issues based on troubleshooting documentations. 

:::image type="content" source="media/17668422-troubleshooting-dash.png" alt-text="Screenshot of new troubleshooting dashboard in console.":::

For more information, see [Software update health dashboard.](../../clients/manage/software-update-health-dashboard.md)

### Introducing centralized search box: Effortlessly find what you need in the console!

Users can now use the global search box in CM console, which streamlines the search experience and centralizes access to information. This feature enhances the overall usability, productivity and effectiveness of CM. Users no longer need to navigate through multiple nodes or sections/ folders to find information they require, saving valuable time and effort.

:::image type="content" source="media/24501008-search-box.png" alt-text="Screenshot of centralized search box in console.":::

For more information, see [Improvements to console search.](../../servers/manage/admin-console-tips.md#improvements-to-console-search)

### Added Folder support for Scripts node in Software Library 

You can now organize scripts by using folders. This change allows for better categorization and management of scripts. Full Administrator and Operations Administrator roles can manage the folders. 

:::image type="content" source="media/24475159-folder-scripts.png" alt-text="Screenshot of scripts folder structure in console.":::

For more information, see [Folder support for scripts.](../../../apps/deploy-use/create-deploy-scripts.md#folder-support-for-scripts)

### HTTPS or Enhanced HTTP should be enabled for client communication from this version of Configuration Manager

HTTP-only communication is deprecated, and support is removed from this version of Configuration Manager. Enable HTTPS or Enhanced HTTP for client communication.

For more information, see [Enable site system roles for HTTPS or Enhanced HTTP.](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http) and [Deprecated features](deprecated/removed-and-deprecated-cmfeatures.md)


### Windows Server 2012/2012 R2 operating system site system roles are not supported from this version of Configuration Manager

Starting 2403, Windows Server 2012/2012 R2 operating system site system roles aren't supported in any CB releases. Clients with extended support (ESU) will continue to support.

For more information, see [Supported-operating-systems-for-site-system-servers.](../configs/supported-operating-systems-for-site-system-servers.md)

### Resource access profiles and deployments will block Configuration manager upgrade

Any configured Resource access profiles and deployments block Configuration manager upgrade. Consider deleting them and moving the co-management workload for Resource Access (if co-managed) to Intune.

For more information, see [FAQ](../../../../configmgr/protect/plan-design/resource-access-deprecation-faq.yml) and [Resource access policies are no longer supported.](../../servers/deploy/install/list-of-prerequisite-checks.md)

## Software updates

### New parameter SoftwareUpdateO365Language is added to Save-CMSoftwareUpdate cmdlet

A new parameter **SoftwareUpdateO365Language** is now added to PowerShell  Save-CMSoftwareUpdate cmdlet. Customers now don't have to check a specific language in the SUP Properties (causing a metadata download for that language for all updates). 


PowerShell Commandlet:  ``` Save-CMSoftwareUpdate – SoftwareUpdateO365Language <language name> (<region name>)" ```

> [!NOTE]
> Languages need to be in O365 format to be consistent with Admin Console UI. E.g. "Hungarian (Hungary)". 



## OS deployment

### Support for ARM 64 Operating System Deployment

Configuration Manager operating system deployment support is now added on Windows 11 ARM 64 devices. Currently Importing and customizing Arm 64 boot images, Wipe and load TS, Media creation TS, WDS PXE for Arm 64 and CMPivot is supported.    

:::image type="content" source="media/14959666-armosd.png" alt-text="Screenshot of arm 64 boot image in console.":::



### Enhancement in Deploying Software Packages with Dynamic Variables  

When deploying a Task Sequence for installing a software package using dynamic variables, if the 'Continue on error' option is unchecked and the package is updated on distribution points while the client is installing the Task Sequence, the installation process fails due to version inconsistencies with the updated packages on the distribution points. Previously, the only recourse was to reinstall the entire Task Sequence from the software center.

To address this issue, we've introduced a new feature allowing administrators to specify the number of retries the system should attempt before marking the Task Sequence as failed. This retry mechanism is activated only when the 'Continue on error' checkbox is unchecked."

:::image type="content" source="media/24334765-dyn-var.png" alt-text="Screenshot of changes in dynamic variable in task sequence in CM console.":::

For more information, see [Options for Install Application.](../../../osd/understand/task-sequence-steps.md#retry-this-step-if-computer-unexpectedly-restarts)

## Cloud-attached management

### Upgrade to CM 2403 is blocked if CMG V1 is running as a cloud service (classic)

The option to upgrade Configuration Manager 2403 is blocked if you're running cloud management gateway V1 (CMG) as a cloud service (classic). All CMG deployments should use a virtual machine scale set.

For more information, see [Check for a cloud management gateway (CMG) as a cloud service (classic).](../../servers/deploy/install/list-of-prerequisite-checks.md)

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

- System Center Update Publisher (SCUP) and integration with ConfigMgr planned end of support Jan 2024.

For more information, see [Removed and deprecated features for Configuration Manager.](deprecated/removed-and-deprecated-cmfeatures.md).

## Other updates

#### Improvements to Bitlocker

This release includes the following improvements to Bitlocker:

- Starting in this release, this feature ensures proper verification of key escrow and prevents message drops. We now validate whether the key is successfully escrowed to the database, and only on successful escrow we add the key protector.
- This feature now prevents a potential data loss scenario where BitLocker is protecting the volumes with keys that are never backed up to the database, in any failures to escrow happens.

For more information on BitLocker management, see [Deploy BitLocker management.](../../../protect/deploy-use/bitlocker/recovery-service.md) and [Plan for BitLocker management.](../../../protect/plan-design/bitlocker-management.md).

- From this version of Configuration Manager, the Windows 11 readiness dashboard shows charts for Windows 23H2.
- Defender Exploit Guards policy for controlled folder now accepts regex in the file path for apps.  
  For example, [C:\Folder\Subfolder\app?.exe] [C:\Folder1\Sub*Name]

## Next steps
<!--At this time, version 2403 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2403.md#early-update-ring).-->

As of May 06, 2024, version 2403 is globally available for all customers to install.
>[!NOTE] 
> For exisiting Fast ring current branch 2403 customers, you will see Slow ring upgrade package in console. Install 2403 Slow ring package to be in production current branch.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2403](../../servers/manage/checklist-for-installing-update-2403.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2403.md#post-update-checklist).
