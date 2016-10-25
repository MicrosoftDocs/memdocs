---
title: "Changes from Configuration Manager 2012 | System Center Configuration Manager "
description: "Identify the changes and new capabilities in System Center Configuration Manger versus System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brendunsms.author: brendunsmanager: angrobe

---
# What&#39;s changed in System Center Configuration Manager from System Center 2012 Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager current branch introduces important changes from System Center 2012 Configuration Manager. The information in this topic identifies the more significant changes and new capabilities found in the baseline version 1511 of System Center Configuration Manager. To learn about additional changes that are introduced in subsequent updates for System Center Configuration Manager, see [What’s new in System Center Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 The December 2015 release of System Center Configuration Manager (version 1511), is the latest product release of Configuration Manager from Microsoft.   It is typically referred to as System Center Configuration Manager current branch. *Current branch* indicates this is a version that supports incremental updates to the product and can be an important distinction between this and past releases of Configuration Manager.  

 With this release System Center Configuration Manager:  

-   Does not  use a year or product identifier in the product name, as seen with past versions like Configuration Manager 2007 or System Center 2012 Configuration Manager.

-   Supports incremental in-product  updates, also called update versions. The initial release is version 1511. Subsequent versions are released several times a year as in-console updates, like version 1602 or 1606.




##  <a name="bkmk_updates"></a> In-console updates for Configuration Manager  
 System Center Configuration Manager uses an in-console service method called **Updates and Servicing** that makes it easy to locate and then install recommended updates for Configuration Manager.  

 Some versions are only available as updates for existing sites (from within the Configuration Manager console), and cannot be used to install new Configuration Manager sites.   
For example, the 1602 update is only available from within the Configuration Manager console and is used to update a site that runs a baseline version of 1511 to version 1602.  

Periodically, an update version will also be released as a new baseline version (like update 1606) which can be used to install a new hierarchy without the need to start with an older baseline version (like 1511) and upgrade your way to the most current version.


 For more information about using updates, see [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md).  

##  <a name="bkmk_servicepoint"></a> Service connection point replaces Microsoft Intune connector  
 The **Microsoft Intune connector** is replaced by a new site system role that enables additional functionality, the **service connection point**. The service connection point:  

-   Replaces the Microsoft Intune connector when you integrate Intune with System Center Configuration Manager On\-premises Mobile Device Management  

-   Is used as a point of contact for devices you manage with  

-   Uploads usage data about your deployment to the Microsoft cloud service  

-   Makes updates that apply to your deployment available from within the Configuration Manager console  

This site system role supports both an online and offline mode of operation that can affect its additional use. For more information see [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Usage data collection  
 System Center Configuration Manager collects usage data about your sites and infrastructure. This information is compiled and submitted to the Microsoft cloud service by the service connection point (a new site system role) and is required to enable Configuration Manager to download updates for your deployment that apply to the version of Configuration Manager you use. When you configure the service connection point you can configure both the level of data that is collected, and whether this is submitted automatically (online mode) or manually (offline mode).  

 For more information see [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Support for Intel Active Management Technology (AMT)  
 With System Center Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

-   AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   Use of the add-on provides you access to the latest capabilities to manage AMT while removing limitations introduced until Configuration Manager could incorporate those changes  

-   Out of Band Management in System Center 2012 Configuration Manager is not affected by this change  

The removal of integrated AMT for System Center Configuration Manager includes:  

-   The Out of Band Management point site system role is no longer used nor available  

##  <a name="bkmk_out"></a> Deprecated functionality  
 With System Center Configuration Manager, some capabilities, like native [Support for Intel Active Management Technology (AMT)](#bkmk_AMT) based-computers is removed from the Configuration Manager console, while other capabilities like Network Access Protection are removed entirely. Additionally, some older Microsoft products like Windows Vista,  Windows Server 2008, and SQL Server 2008, are no longer supported.  

 For a list of deprecated features, see [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 For details about supported products, operating systems, and configurations, see [Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## Client deployment  
 System Center Configuration Manager introduces a new capability for testing new versions of  the Configuration Manager client before upgrading the rest of site with the new software.  This new capability gives you the opportunity to set up a preproduction collection in which to pilot a new client. Once you are satisfied with the new client software in preproduction, you can promote the client to automatically upgrade the rest of the site with the new version.  

 For more information on how to test clients, see [How to test client upgrades in a preproduction collection in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## Operating system deployment  

-   A  new task sequence type is available in the Create Task Sequence Wizard,  **Upgrade an operating system from upgrade package**, that creates the steps to upgrade computers from Windows 7, Windows 8, or Windows 8.1 to Windows 10.  For more information, see [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Windows PE Peer Cache is now available when you deploy operating systems. Computers that run a task sequence to deploy an operating system can use Windows PE Peer Cache to obtain content from a local peer (a peer cache source) instead of downloading content from a distribution point. This helps minimize wide area network (WAN) traffic in branch office scenarios where there is no local distribution point. For more information, see [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   You can now view the state of Windows as a Service in your environment, create servicing plans to form deployment rings and ensure that Windows 10 current branch computers are kept up to date when new builds are released, and view alerts when Windows 10 clients are near end of support for their build of Current Branch (CB) or Current Branch for Business (CBB). For more information, see [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## Application management  

-   System Center Configuration Manager lets you deploy Universal Windows Platform (UWP) apps for devices running Windows 10 and later. See [Creating Windows applications with System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Software Center has a new, modern look and apps that previously only appeared in the Application Catalog (user-available apps) now appear in Software Center under the Applications tab. This makes these deployments more discoverable to users and removes the need for them to use the Application Catalog. Additionally, a Silverlight enabled browser is no longer required. See [Plan for and configure application management in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   The new Windows Installer through MDM application type lets you create and deploy Windows Installer-based apps to enrolled PCs that run Windows 10. See [Creating Windows applications with System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   When you create an application for an in-house iOS app you only need to specify the installer (.ipa) file for the app. You no longer need to specify a corresponding property list (.plist) file. See [Creating iOS applications with System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   In Configuration Manager 2012, to specify a link to an app in the Windows Store, you could either specify the link directly, or browse to a remote computer that had the app installed. In System Center Configuration Manager, you can still enter the link directly, but now, instead of browsing to a reference computer, you can now browse the store for the app directly from the Configuration Manager console.  

## Software updates  

-   System Center Configuration Manager can now differentiate a Windows 10 computer that connects to  Windows Update for Business (WUfB) for software update management versus the computers connected to WSUS for software update management. The **UseWUServer** attribute is new and specifies whether the computer is managed with WUfB. You can use this setting in a collection to remove these computers from software update management. For more information, see [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   You can now schedule and run the WSUS clean up task from the Configuration Manager console.  
    You can now manually run the WSUS cleanup task from in Software Update Point Component properties. When you select to run the WSUS cleanup task, it will run at the next software updates synchronization. The expired software updates will be set to a status of declined on the WSUS server and the Windows Update Agent on computers will no longer scan these software updates. For more information, see [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## Compliance settings  

-   System Center Configuration Manager introduces an improved workflow for creating configuration items. Now, when you create a configuration item, and select supported platforms, only the settings relevant to that platform are available. See [Get started with compliance settings in System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   The create configuration item wizard now makes it easier to choose the configuration item type you want to create. Additionally, new and updated configuration items are available for:  

    -   Windows 10 devices managed with the Configuration Manager client  

    -   Mac OS X devices managed with the Configuration Manager client  

    -   Windows desktop and server computers managed with the Configuration Manager client  

    -   Windows 8.1 and Windows 10 devices managed without the Configuration Manager client  

    -   Windows Phone devices managed without the Configuration Manager client  

    -   iOS and Mac OS X devices managed without the Configuration Manager client  

    -   Android and Samsung KNOX devices managed without the Configuration Manager client  

     See [How to create configuration items in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Support for managing settings on Mac OS X computers that are either enrolled with Microsoft Intune or managed using the Configuration Manager client. See [How to create configuration items for iOS and Mac OS X devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## Protect data and site infrastructure  
-   System Center Configuration Manager lets you integrate with Windows Hello for Business (formerly Microsoft Passport for Work) which is an alternative sign-in method that uses Active Directory, or an Azure Active Directory account to replace a password, smart card, or virtual smart card on devices running Windows 10. See [Windows Hello for Business settings in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## Mobile device management with Microsoft Intune  
 System Center Configuration Manager introduces improvements to the mobile device management experience including:  

-   Limit the number of devices a user can enroll  

-   Specify terms and conditions users of the Company Portal must accept before they can enroll or use the app  

-   Added a device enrollment manager role to help manage large numbers of devices  

For more information about mobile device management capabilities with Configuration Manager and Intune, see [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

## On-premises Mobile Device Management  
 With System Center Configuration Manager, you can now manage mobile devices using on-premises Configuration Manager infrastructure. All device management and management data is handled on-premises and is not part of Microsoft Intune or other cloud services. This type of device management doesn't require client software since the capabilities that Configuration Manager uses to manage the devices are built into the device operating systems.  

 To learn more, see [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).
