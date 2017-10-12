---
title: "Create iOS applications"
titleSuffix: "Configuration Manager"
description: "See which considerations you must take into account when you create and deploy applications for iOS devices."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: 10
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Create iOS applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A System Center Configuration Manager application has one or more deployment types that comprise the installation files and information that are required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

 You can create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  

-   Manually create the application and then add deployment types later.  

-   Import an application from a file.  

See [Start the create application wizard](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) for the steps required to create Configuration Manager applications and deployment types. Also, keep the following considerations in mind when you create and deploy applications for iOS devices.  

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
