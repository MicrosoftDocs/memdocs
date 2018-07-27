---
title: Create iOS applications
titleSuffix: Configuration Manager
description: How to create and deploy applications for iOS devices in Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create iOS applications in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A Configuration Manager application has one or more deployment types that comprise the installation files and information that are required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

See [create an application](/sccm/apps/deploy-use/create-applications#bkmk_create) for the steps to create Configuration Manager applications and deployment types. 

Keep in mind the following considerations when you create and deploy applications for iOS devices:  

- Configuration Manager supports the deployment of iOS .ipa packages. You don't need to specify a property list (.plist) file when importing an iOS app. 

- Deploy iOS applications as **Available** or **Required**. The user must consent to both installation and uninstallation.

> [!IMPORTANT]  
>  Currently, end-users can't install corporate apps from the Microsoft Intune Company Portal app for iOS. This limitation is because there are restrictions on apps published in the iOS App Store. (See the App Store Review Guidelines, Section 2). Users can install corporate apps by browsing to the Intune portal on their device. These apps include managed App Store apps and line-of-business app packages. For more information about the mobile management capabilities that the Intune Company Portal app enables, see [Enrolled device management capabilities in Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  
