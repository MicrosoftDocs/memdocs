---
title: "Create iOS applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for iOS devices."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsftms.author: robstackmanager: angrobe

---
# Create iOS applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Keep the following considerations in mind when you create and deploy applications for iOS devices.  

## General considerations  
 Configuration Manager supports the deployment of the following app types:  

|Device type|Supported files|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> In System Center Configuration Manager, you do not need to specify a property list (.plist) file when importing an iOS app.|  

 The following deployment actions are supported:  

|Device type|Supported actions|  
|-----------------|-----------------------|  
|iOS|**Available**, **Required**. The user must consent to both installation and uninstallation.

> [!IMPORTANT]  
>  Currently, end-users cannot install corporate apps from the Microsoft Intune Company Portal app for iOS. This is because there are restrictions that are placed on apps that are published in the iOS App Store (see App Store Review Guidelines, Section 2). Users can install corporate apps (including managed App Store apps and line-of-business app packages) by browsing to the Intune Web Portal on their device (portal.manage.microsoft.com). For more information about the mobile management capabilities that are enabled by the Intune Company Portal app, see [Enrolled device management capabilities in Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  
