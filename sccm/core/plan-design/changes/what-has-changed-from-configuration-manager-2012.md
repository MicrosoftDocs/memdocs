---
title: Changes from Configuration Manager 2012 
description: Identify the changes and new capabilities in System Center Configuration Manger versus System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What's changed in System Center Configuration Manager from System Center 2012 Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The current branch of Configuration Manager introduces important changes from System Center 2012 Configuration Manager. This article identifies significant changes and new capabilities found in the baseline version 1511 of System Center Configuration Manager. To learn about changes introduced in subsequent updates for System Center Configuration Manager, see [What’s new in System Center Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions).

The December 2015 release of System Center Configuration Manager (version 1511) was the initial release of the current Configuration Manager product from Microsoft. It's typically referred to as System Center Configuration Manager current branch. *Current branch* indicates this version supports incremental updates to the product. It also provides a way to distinguish between this release and previous releases of Configuration Manager.  

System Center Configuration Manager:  

- Doesn't use a year or product identifier in the product name, unlike past versions such as Configuration Manager 2007 or System Center 2012 Configuration Manager.  

- Supports incremental, in-product updates, also called update versions. The initial release was version 1511. Subsequent versions are released several times a year as in-console updates, like version 1710.  

- Is installed using a baseline version. While 1511 was the original baseline version, new baseline versions are also released from time to time, like 1802. Baseline versions can be used to install a new System Center Configuration Manager site and hierarchy or to upgrade from a supported version of Configuration Manager 2012.  



##  <a name="bkmk_updates"></a> In-console updates for Configuration Manager  

System Center Configuration Manager uses an in-console service method called **Updates and Servicing** that makes it easy to locate and install recommended updates.  

Some versions are only available as updates for existing sites (from within the Configuration Manager console), and can't be used to install new Configuration Manager sites. For example, the 1710 update is only available from within the Configuration Manager console. It's used to update a site that already runs a version of System Center Configuration Manager.

Periodically, an update version is also released as a new baseline version (like update 1802). This kind of update can be used to install a new hierarchy, without the need to start with an older baseline version (like 1511) and upgrade your way to the most current version.


For more information about using updates, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).  
For more information about baselines, see [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).



##  <a name="bkmk_servicepoint"></a> New site system role: service connection point  

The **Microsoft Intune connector** is replaced by a new site system role that enables additional functionality, the **service connection point**. The service connection point:  

- Replaces the Microsoft Intune connector when you integrate Intune with System Center Configuration Manager on-premises mobile device management.  

- Is used as a point-of-contact for devices you manage.  

- Uploads usage data about your deployment to the Microsoft cloud service.  

- Makes updates that apply to your deployment available from within the Configuration Manager console.  

This site system role supports both online and offline modes of operation. For more information, see [About the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  



##  <a name="bkmk_usage"></a> Usage data collection  

Configuration Manager collects usage data about your sites and infrastructure. This information is compiled and submitted to the Microsoft cloud service by the service connection point. It's required to enable Configuration Manager to download updates for your deployment that apply to the version of Configuration Manager you use. When you set up the service connection point, you can specify both the level of data that is collected, and whether the data is submitted automatically (online mode) or manually (offline mode).  

For more information, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



##  <a name="bkmk_AMT"></a> Support for Intel Active Management Technology (AMT)  

Configuration Manager current branch removes native support for AMT-based computers from within the Configuration Manager console. AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

The removal of integrated AMT for Configuration Manager includes out-of-band management. The out-of-band management point site system role is no longer available.  

> [!Note]   
> Out-of-band management in System Center 2012 Configuration Manager isn't affected by this change.  



##  <a name="bkmk_out"></a> Deprecated functionality  

Some features, like native [Support for Intel Active Management Technology (AMT)](#bkmk_AMT) based-computers, are removed from the Configuration Manager console. Other features, like Network Access Protection, are removed entirely. Additionally, some older Microsoft products like Windows Vista, Windows Server 2008, and SQL Server 2008, are no longer supported.  

For a list of deprecated features, see [Removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).  

For details about supported products, operating systems, and configurations, see [Supported configurations](/sccm/core/plan-design/configs/supported-configurations).  



## Client deployment  

Configuration Manager introduces a new feature for testing new versions of the Configuration Manager client before upgrading the rest of site with the new software. You can set up a pre-production collection in which to pilot a new client. Once you're satisfied with the new client software in pre-production, you can promote the client to automatically upgrade the rest of the site with the new version.  

For more information on how to test clients, see [How to test client upgrades in a pre-production collection](/sccm/core/clients/manage/upgrade/test-client-upgrades).  



## OS deployment  

Be aware of the following changes to OS deployment:

- In the Create Task Sequence Wizard, a new task sequence type is available: **Upgrade an operating system from upgrade package**. It creates the steps to upgrade computers from Windows 7, Windows 8, or Windows 8.1 to Windows 10. For more information, see [Upgrade Windows to the latest version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Windows PE peer cache is now available when you deploy operating systems. Computers that run a task sequence to deploy an OS can use Windows PE peer cache to obtain content from a peer cache source, instead of downloading content from a distribution point. This behavior helps minimize WAN traffic in branch office scenarios where there's no local distribution point. For more information, see [Prepare Windows PE peer cache to reduce WAN traffic](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

- You can now view the state of Windows as a service in your environment. You can also create servicing plans to form deployment rings, and make sure that Windows 10 current branch computers are kept up-to-date when new builds are released. Additionally, you can view alerts when Windows 10 clients are near the end of support for their build. For more information, see [Manage Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service).  



## Application management  

Be aware of the following changes to application management:

- Configuration Manager lets you deploy Universal Windows Platform (UWP) apps for devices running Windows 10 and later. For more information, see [Creating Windows applications](/sccm/apps/get-started/creating-windows-applications).  

- Software Center has a new, modern look. User-available apps that previously only appeared in the application catalog now appear in Software Center under the Applications tab. This behavior makes these deployments more discoverable, and makes it unnecessary for users to refer to the application catalog. Additionally, a Silverlight-enabled browser is no longer required. For more information, see [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

- The new Windows Installer through MDM application type lets you create and deploy Windows Installer-based apps to enrolled PCs that run Windows 10. For more information, see [Creating Windows applications](/sccm/apps/get-started/creating-windows-applications).  

- When you create an application for an in-house iOS app, you only need to specify the installer (.ipa) file for the app. You no longer need to specify a corresponding property list (.plist) file. See [Creating iOS applications](/sccm/apps/get-started/creating-ios-applications).  

- In Configuration Manager 2012, to specify a link to an app in the Windows Store, you could either specify the link directly, or browse to a remote computer that had the app installed. In Configuration Manager current branch, you can still enter the link directly, but now, instead of browsing to a reference computer, you can browse the store for the app directly from the Configuration Manager console.  



## Software updates  

Be aware of the following changes to software updates:

- Configuration Manager can now detect the difference between software update management methods for computers. Specifically, it can differentiate between a Windows 10 computer that connects to Windows Update for Business (WUfB), and a computer connected to WSUS. The **UseWUServer** attribute is new, and specifies whether the computer is managed with WUfB. You can use this setting in a collection to remove these computers from software update management. For more information, see [Integration with Windows Update for Business in Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).  

- You can now schedule and run the WSUS clean-up task from the Configuration Manager console. In **Software Update Point Component** properties, when you select to run the WSUS clean-up task, it runs at the next software updates synchronization. The expired software updates are set to a status of declined on the WSUS server, and the Windows Update Agent on computers no longer scans these software updates. For more information, see [Schedule and run the WSUS clean up task](/sccm/sum/deploy-use/software-updates-maintenance).  



## Compliance settings  

Be aware of the following changes to compliance settings:

- Configuration Manager improves the workflow for creating configuration items. Now, when you create a configuration item, and select supported platforms, only the settings relevant to that platform are available. See [Get started with compliance settings](/sccm/compliance/get-started/get-started-with-compliance-settings).  

- The **Create Configuration Item** wizard now makes it easier to choose the configuration item type you want to create. Additionally, new and updated configuration items are available for:  

    - Windows 10 devices managed with the Configuration Manager client  

    - Mac OS X devices managed with the Configuration Manager client  

    - Windows desktop and server computers managed with the Configuration Manager client  

    - Windows 8.1 and Windows 10 devices managed without the Configuration Manager client  

    - Windows Phone devices managed without the Configuration Manager client  

    - iOS and Mac OS X devices managed without the Configuration Manager client  

    - Android and Samsung KNOX Standard devices managed without the Configuration Manager client  
  
    For more information, see [How to create configuration items](/sccm/compliance/deploy-use/create-configuration-items).  

- Support for managing settings on Mac OS X computers that are either enrolled with Microsoft Intune or managed with the Configuration Manager client. See [How to create configuration items for iOS and Mac OS X devices managed without the Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).  



## On-premises mobile device management  

You can now manage mobile devices by using on-premises Configuration Manager infrastructure. All device and management data are handled on-premises, and isn't part of Microsoft Intune or other cloud services. This type of device management doesn't require client software. Configuration Manager manages devices with functionality that's built into the device OS.  

For more information, see [Manage mobile devices with on-premises infrastructure](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).
