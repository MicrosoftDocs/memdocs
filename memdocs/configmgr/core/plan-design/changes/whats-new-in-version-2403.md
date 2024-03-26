---
title: What's new in version 2403
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2403 of Configuration Manager current branch.
ms.date: 03/28/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2403 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2403 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2211 or later. This article summarizes the changes and new features in Configuration Manager, version 2403.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2309](../../servers/manage/checklist-for-installing-update-2309.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2309.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure

### Microsoft Azure Active Directory re-branded to Microsoft Entra ID

Starting Configuration Manager version 2403, Microsoft Azure Active Directory is re-named to Microsoft Entra ID within Configuration Manager. 

### Automated diagnostic Dashboard for Software Update Issues

A new dashboard is added to the console under monitoring workspace which shows the diagnosis of the software update issues in your environment. You can fix software update issues based on troubleshooting documentations.


### Introducing Centralized Search box: Effortlessly Find What You Need in the Console!

Users can now use the global search box in CM console which streamlines the search experience and centralizes access to information. This enhances the overall usability, productivity and effectiveness of CM. Users no longer need to navigate through multiple nodes or sections/ folders to find information they require, saving valuable time and effort.


### Added Folder support for Scripts node in Software Library 

You can now organize scripts by using folders. This change allows for better categorization and management of scripts. Full Administrator and Operations Administrator roles can manage the folders. 

### HTTPS or Enhanced HTTP should be enabled for client communication from this version of Configuration Manager

HTTP-only communication is deprecated, and support is removed from this version of Configuration Manager. Please enable HTTPS or Enhanced HTTP for client communication.


### Windows Server 2012/2012 R2 operating system site system roles are not supported from this version of Configuration Manager

Starting 2403, Windows Server 2012/2012 R2 operating system site system roles are not supported in any CB releases. Clients with extended support (ESU) will continue.  

### Resource access profiles and deployments will block Configuration manager upgrade

Any configured Resource access profiles and associated deployments will block the Configuration manager upgrade. Please consider deleting them and moving the co-management workload for Resource Access (if co-managed) to Intune.


## Software updates

### New parameter SoftwareUpdateO365Language is added to Save-CMSoftwareUpdate cmdlet

A new parameter for SoftwareUpdate O365Language is added to Powershell Save-CMSoftwareUpdate cmdlet. Customers now do not, have to check for a specific language in the SUP properties from console (earlier causing a metadata download for that language for all updates).

PowerShell Commandlet: Save-CMSoftwareUpdate – SoftwareUpdateO365Language <language name> (<region name>)"



## OS deployment

### Support for ARM64 Operating System Deployment

Configuration Manager operating system deployment support is now added on Windows 11 ARM64 devices. Currently Importing and customizing Arm64 boot images, Wipe and load TS, Media creation TS, and WDS PXE for Arm64 is supported.    

### Enhancement in Deploying Software Packages with Dynamic Variables  

Administrators while deploying the "Install Software Package" via Dynamic variable with "Continue on error" unchecked to clients, will not be notified with task sequence failures even if package versions on the distribution point are updated.



## Cloud-attached management

### Upgrade to CM 2403 is blocked if CMG V1 is running as a cloud service (classic)

The option to upgrade Configuration Manager 2403 is blocked if you are running cloud management gateway V1 (CMG) as a cloud service (classic). All CMG deployments should use a virtual machine scale set. For more information see ,


## Deprecated features

### System Center Update Publisher (SCUP) and integration with ConfigMgr 

## Other updates


## Next steps
At this time, version 2403 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2309.md#early-update-ring).-->

<--! As of March 28, 2024, version 2403 is globally available for all customers to install.-->

>[!NOTE] 
> For exisiting Fast ring current branch 2403 customers, you will see Slow ring upgrade package in console. Install 2403 Slow ring package to be in production current branch.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2309](../../servers/manage/checklist-for-installing-update-2309.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2309.md#post-update-checklist).
