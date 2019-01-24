---
title: "Capabilities in Technical Preview 1602"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1602."
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
---
# Capabilities in Technical Preview 1602 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1602. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

 The following are new features you can try out with this version.  

##  <a name="BKMK_MDM"></a> Improvements to mobile device management  

### iOS Activation Lock  
 System Center Configuration Manager can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. Activation Lock is enabled automatically when the Find My iPhone app is used on a device. After it is enabled, the user's Apple ID and password must be entered before anyone can:  

- Turn off Find My iPhone  

- Erase the device  

- Reactivate the device  

  Configuration Manager can request the Activation Lock status of both supervised and unsupervised devices that run iOS 7.1 and later. For supervised devices, Intune can retrieve the Activation Lock bypass code and directly issue it to the device.  

  For details, see [Help protect iOS devices with Activation Lock bypass for Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a> Improvements to Software Center in version 1602  

### Refresh PC machine and user policy from Software Center  
 A new option, **Sync Policy** has been added to the **Options** > **Computer Maintenance** page of Software Center that causes the PC to refresh it’s Configuration Manager machine and user policy.  

##  <a name="BKMK_Win10Servicing"></a> Improvements to Windows 10 Servicing  
 In the 1602 Technical Preview we have added the following improvements for Windows 10 Servicing:  

-   New filter options for Servicing Plans.  You can now filter for **Language**, **Required**, and **Title**. Only upgrades that meet the specified criteria will be added to the associated deployment.  

-   When you select the **Upgrades** classification for software updates synchronization, a warning dialog is displayed to let you know that WSUS [hotfix 3095113](https://support.microsoft.com/kb/3095113) is required to successfully synchronize software updates and for the Windows 10 Servicing  to work properly.  From the dialog, you can go to the knowledge base article for the hotfix.  

-   Available Windows 10 upgrades now only display in the **Windows 10 Servicing** \ **All Windows 10 Updates** node of the Configuration Manager console. These updates no longer display in the **Software Updates** \ **All Software Updates** node.  

-   End-users that start a Windows 10 Upgrade package will be prompted with a dialog that lets them know they will be upgrading their operating system.  
