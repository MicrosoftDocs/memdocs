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

Update 2403 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2211 or later. This article summarizes the changes and new features in Configuration Manager, version 2309.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2309](../../servers/manage/checklist-for-installing-update-2309.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2309.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure

### Introducing SQL ODBC driver support for Configuration Manager

Starting with Configuration Manager 2403 release, Configuration Manager requires the installation of the ODBC driver for SQL server 18.1.0 or later as a prerequisite. This prerequisite is required when you create a new site or update an existing one and on all remote roles.


### Option to schedule scripts' runtime



### External service notification Run details from Azure Logic application  


### New Site Maintenance task “Delete Aged Task Execution Status Messages” is now available on primary servers to clean up data older than 30 days or configured number of days


## Software updates

### Update Orchestrator Service (USO) for Windows 11 22H2 or later with windows native reboot experience 


### Maintenance window creation using PS cmdlet 



## OS deployment

### OSD preferred MP option for PXE boot scenario  


### Enable Bitlocker through ProvisionTS  


### Windows 11 Edition Upgrade using CM Policy settings 


### Windows 11 Upgrade Readiness Dashboard 


## Cloud-attached management

### New Cloud Management Gateway (CMG) creation via Console 


### New Cloud Management Gateway (CMG) creation via PowerShell 


## Deprecated features


## Other updates


## Next steps
At this time, version 2403 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2309.md#early-update-ring).-->

As of March 28, 2024, version 2403 is globally available for all customers to install.

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
