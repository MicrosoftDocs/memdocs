---
title: What's new in version 2409
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2409 of Configuration Manager current branch.
ms.date: 12/03/2024
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

# What's new in version 2409 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2409 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2309 or later. <!--When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability.--> This article summarizes the changes and new features in Configuration Manager, version 2409.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2409](../../servers/manage/checklist-for-installing-update-2409.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2409.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure
<!--24501008-->
### Configuration Manager now supports SQL Extended Protection for Authentication

Configuration Manager now supports SQL extended protection for authentication. It's a security feature that enhances protection against MITM attacks, making SQL server more secure when connections are made using extended protection. These enhancements collectively reduce the risk of unauthorized access and protect sensitive data managed by the SQL Server database engine. 

For more information, see [Connect to the Database Engine Using Extended Protection](/sql/database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection)

###  Introducing Centralized Search - Desired Workspace Selection
<!--27679763-->
The centralized search box now enables the option to select the desired workspace for searching. Users can easily refine their search results by selecting the desired workspace from the dropdown menu.

:::image type="content" source="media/27679763-search-workspace.png" alt-text="Screenshot of centralized search workspace selection in console." lightbox="media/27679763-search-workspace.png":::

### Configuration Manager does not support SQL Server 2012 and 2014

Starting with version 2409, Configuration Manager no longer supports SQL Server 2012 and 2014. Upgrade to the latest SQL Server version or at least SQL Server 2016. If you don’t upgrade, CM upgrades are blocked, and you see an error during the prereq check. 

<!--## Software updates-->

### Operating System support added for Windows 11 24H2 and Windows Server 2025

With this version of Configuration Manager, support is added for Windows 11 24H2 and Windows Server 2025.
 - Windows 11 24H2 & Windows Server 2025 are added to the Product lifecycle dashboard and supported platform.
 - Windows 11 24H2 & Windows Server 2025 client support is added.
 - Boot image creation in CM on Windows Server 2025 now supports latest Windows ADK.
 - Windows upgrade readiness dashboard now supports Windows 11 24H2 for upgrading clients.
   
>[!NOTE]
>Windows Server and Windows 11 24H2 do not support Firewall Rules. This will result in a non-compliant status in the Configuration Manager applet.


### Software metering support in Arm64 devices

The Configuration Manager now supports Software metering for Arm64 devices. Software metering is used to monitor Windows PC desktop apps with a filename ending in .exe. For more information, see [Software metering in Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)


## OS deployment

### BitLocker support in Arm64 devices

Configuration Manager now supports BitLocker task sequence steps for Arm64 devices. In BitLocker Management, policies that include OS drive encryption with a TPM protector and fixed drive encryption with the Auto-Unlock option are supported on Arm64 devices.

For more information , see [Bitlocker Supported configurations](../../../protect/plan-design/bitlocker-management.md#supported-configurations)

## Cloud-attached management

### CMG Entra Application secret key renewal  

The 'Renew Secret Key' feature now opens a dialog with four options for the validity period. This update also prevents applications older than 800 days (approximately two years) from renewing their secret keys. The same options are available when creating a new app. 

:::image type="content" source="media/27297018-secret-window.png" alt-text="Screenshot of secret window selection in console.":::

>[!NOTE]
>The admin must sign in using tenant global administrator credentials and then click on the Renew button.

### CMG Enhanced security option

CMG Setup now uses managed Identities and third-party **Server App** to interact with CMG's Azure Storage account, instead of storage account keys. 

 - Hence storage account key access is disabled for new CMG setup.
 - For sessions upgrading from earlier versions to 2409, the 'CMG enhanced security' button is shown as enabled.

 :::image type="content" source="media/27297018-Cmg-Enhanced.png" alt-text="Screenshot of Cmg enhanced window selection in console." lightbox="media/27297018-Cmg-Enhanced.png":::

## Known Issues

 - Upgrade SQL 2012 or 2014 Express, Standard, Enterprise edition to SQl 2016 or latest version. **VC++ Redistributable Version** need to be upgraded to latest version on **Secondary sites**. [Download Latest Microsoft Visual C++ Redistributable Version](https://aka.ms/vs/17/release/vc_redist.x64.exe).

 - Site base bootable media in SSL & Non-SSL session using CMG cert will not work. For more information, see [
Create boot media to use a CMG](../../../osd/deploy-use/deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content)

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

For more information, see [Removed and deprecated features for Configuration Manager.](deprecated/removed-and-deprecated-cmfeatures.md).

<!--#### Improvements to Bitlocker-->

## Next steps
At this time, version 2409 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2409.md#early-update-ring).

<!--As of May 06, 2024, version 2403 is globally available for all customers to install.-->
<!-- >[!NOTE] -->
<!-- For exisiting Fast ring current branch 2403 customers, you will see Slow ring upgrade package in console. Install 2403 Slow ring package to be in production current branch.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2409](../../servers/manage/checklist-for-installing-update-2409.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2409.md#post-update-checklist).
