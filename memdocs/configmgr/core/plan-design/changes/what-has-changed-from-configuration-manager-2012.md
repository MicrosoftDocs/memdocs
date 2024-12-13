---
title: Changes from version 2012
titleSuffix: Configuration Manager
description: Identify the changes and new capabilities in Configuration Manger versus System Center 2012 Configuration Manager.
ms.date: 04/05/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's changed from System Center 2012 Configuration Manager

*Applies to: Configuration Manager (current branch)*

The current branch of Configuration Manager introduces important changes from System Center 2012 Configuration Manager. This article identifies significant changes and new capabilities found in the original baseline version 1511 of Configuration Manager current branch. To learn about changes introduced in recent updates for Configuration Manager, see [What's new in Configuration Manager incremental versions](whats-new-incremental-versions.md).

> [!NOTE]
> Since October 2019, Configuration Manager is part of Microsoft Intune family of products. For more information, see [Microsoft Configuration Manager FAQ](../../understand/microsoft-endpoint-manager-faq.yml).

The December 2015 release (version 1511) of Configuration Manager was the initial release of the current Configuration Manager product from Microsoft. It's typically referred to as Configuration Manager current branch. *Current branch* indicates this version supports incremental updates to the product. It also provides a way to distinguish between this release and previous releases of Configuration Manager.  

Configuration Manager current branch:  

- Doesn't use a year or product identifier in the product name, unlike past versions such as Configuration Manager 2007 or System Center 2012 Configuration Manager.  

- Supports incremental, in-product updates, also called update versions. The initial release was version 1511. Later versions are released several times a year as in-console updates, like version 1910.  

- Is installed using a baseline version. While 1511 was the original baseline version, new baseline versions are also released from time to time, like 2203. Baseline versions can be used to install a new Configuration Manager site and hierarchy, or to upgrade from a supported version of System Center 2012 Configuration Manager.  

## <a name="bkmk_updates"></a> In-console updates

Configuration Manager uses an in-console service method called **Updates and Servicing** that makes it easy to locate and install recommended updates.  

Some versions are only available as updates for existing sites from within the Configuration Manager console. You can't use these updates to install a new Configuration Manager site. For example, the 2111 update is only available from within the Configuration Manager console. It's used to update a site that already runs a supported version of Configuration Manager.

Periodically, an update version is also released as a new *baseline* version. For example, update version 2203 is also a baseline. Use a baseline version to install a new site or hierarchy. Don't start with an older baseline version like 2111, and upgrade your way to the most current version. Always use the latest baseline.

For more information, see the following articles:

- [Updates for Configuration Manager](../../servers/manage/updates.md)
- [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="bkmk_servicepoint"></a> Service connection point  

Configuration Manager current branch includes a new site system role, the **service connection point**:  

- A point of contact for many cloud-enabled features

- Downloads updates for your site

- Uploads diagnostics and usage data about your site to the Microsoft cloud

This site system role supports both online and offline modes of operation. For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="bkmk_usage"></a> Diagnostics and usage data

Configuration Manager collects diagnostics and usage data about your sites and infrastructure. This information is compiled and submitted to the Microsoft cloud service by the service connection point. Configuration Manager requires this data to download updates that are applicable for your environment. When you set up the service connection point, you can specify both the level of data that it collects, and whether automatically (online) or manually (offline) submits the data.

For more information, see [Diagnostics and usage data](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="bkmk_out"></a> Deprecated functionality  

Some features, like native [Support for Intel Active Management Technology (AMT)](#bkmk_AMT) based-computers, are removed from the Configuration Manager console. Other features, like Network Access Protection, are removed entirely. Additionally, some older Microsoft products like Windows Vista, Windows Server 2008, and SQL Server 2008, are no longer supported.  

For a list of deprecated features, see [Removed and deprecated items](deprecated/removed-and-deprecated.md).  

For details about supported products, operating systems, and configurations, see [Supported configurations](../configs/supported-configurations.md).  

### <a name="bkmk_AMT"></a> Support for Intel Active Management Technology (AMT)  

Configuration Manager current branch removes native support for AMT-based computers from within the Configuration Manager console. AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

The removal of integrated AMT for Configuration Manager includes out-of-band management. The out-of-band management point site system role is no longer available.  

> [!Note]
> This change doesn't affect out-of-band management in System Center 2012 Configuration Manager.

## Changes in functionality

The following sections summarize some of the significant changes in feature areas between System Center 2012 R2 Configuration Manager and the version 1511 version of Configuration Manager current branch. For more information on more recent changes in functionality, see [What's new in incremental versions](whats-new-incremental-versions.md).

### Client deployment  

Configuration Manager introduces a new feature for testing new versions of the Configuration Manager client before upgrading the rest of site with the new software. You can set up a pre-production collection in which to pilot a new client. Once you're satisfied with the new client software in pre-production, you can promote the client to automatically upgrade the rest of the site with the new version.  

For more information on how to test clients, see [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).  

### OS deployment  

Be aware of the following changes to OS deployment:

- In the Create Task Sequence Wizard, a new task sequence type is available: **Upgrade an operating system from upgrade package**. It creates the steps to upgrade computers from an earlier version of Windows to Windows 10 or later. For more information, see [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Windows PE peer cache is now available when you deploy operating systems. Computers that run a task sequence to deploy an OS can use Windows PE peer cache to obtain content from a peer cache source, instead of downloading content from a distribution point. This behavior helps minimize WAN traffic in branch office scenarios where there's no local distribution point. For more information, see [Prepare Windows PE peer cache to reduce WAN traffic](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- You can now view the state of Windows as a service in your environment. You can also create servicing plans to form deployment rings, and make sure that Windows 10 or later computers are kept up to date when new builds are released. Additionally, you can view alerts when Windows clients are near the end of support for their build. For more information, see [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### Application management  

Be aware of the following changes to application management:

- Configuration Manager lets you deploy Universal Windows Platform (UWP) apps for devices running Windows 10 and later. For more information, see [Creating Windows applications](../../../apps/get-started/creating-windows-applications.md).  

- Software Center has a new, modern look. User-available apps that previously only appeared in the application catalog now appear in Software Center under the Applications tab. This behavior makes these deployments more discoverable, and makes it unnecessary for users to refer to the separate application catalog. Additionally, a Silverlight-enabled browser is no longer required. For more information, see [Plan for and configure application management](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- The new Windows Installer through MDM application type lets you create and deploy Windows Installer-based apps to enrolled PCs that run Windows 10 or later. For more information, see [Creating Windows applications](../../../apps/get-started/creating-windows-applications.md).  

- In Configuration Manager 2012, to specify a link to an app in the Windows Store, you could either specify the link directly, or browse to a remote computer that had the app installed. In Configuration Manager current branch, you can still enter the link directly, but now, instead of browsing to a reference computer, you can browse the store for the app directly from the Configuration Manager console.  

### Software updates  

Be aware of the following changes to software updates:

- Configuration Manager can now detect the difference between software update management methods for computers. Specifically, it can differentiate between a Windows computer that connects to Windows Update for Business, and a computer connected to WSUS. The **UseWUServer** attribute is new, and specifies whether the computer is managed with Windows Update for Business. You can use this setting in a collection to remove these computers from software update management. For more information, see [Integration with Windows Update for Business](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- You can now schedule and run the WSUS clean-up task from the Configuration Manager console. In **Software Update Point Component** properties, when you select to run the WSUS clean-up task, it runs at the next software updates synchronization. The expired software updates are set to a status of declined on the WSUS server, and the Windows Update Agent on computers no longer scans these software updates. For more information, see [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

### Compliance settings  

Be aware of the following changes to compliance settings:

- Configuration Manager improves the workflow for creating configuration items. Now, when you create a configuration item, and select supported platforms, only the settings relevant to that platform are available. See [Get started with compliance settings](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- The **Create Configuration Item** wizard now makes it easier to choose the configuration item type you want to create. Additionally, new and updated configuration items are available for:  

    - Windows 10 or later devices managed with the Configuration Manager client  

    - mac OS X devices managed with the Configuration Manager client  

    - Windows desktop and server computers managed with the Configuration Manager client  

    - Windows 8.1 and Windows 10 or later devices managed without the Configuration Manager client

    For more information, see [How to create configuration items](../../../compliance/deploy-use/create-configuration-items.md).  

- Support for managing settings on macOS X computers that are managed without the Configuration Manager client.

### On-premises mobile device management  

You can now manage mobile devices by using on-premises Configuration Manager infrastructure. All device and management data are handled on-premises, and isn't part of Microsoft Intune or other cloud services. This type of device management doesn't require client software. Configuration Manager manages devices with functionality that's built into the device OS.  

For more information, see [Manage mobile devices with on-premises infrastructure](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## Next steps

[What's new in incremental versions](whats-new-incremental-versions.md)
