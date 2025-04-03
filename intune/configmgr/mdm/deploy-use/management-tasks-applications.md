---
title: Manage apps for on-premises MDM
titleSuffix: Configuration Manager
description: Manage applications for on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: article
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage apps for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you manage devices with Configuration Manager on-premises mobile device management (MDM), you can manage the following application types:

- Windows Phone app package (*.xap file)
- Windows Phone app package (in the Windows Phone Store)
- Windows Installer through MDM
- Web Application

For more general information about managing Configuration Manager applications and deployment types, see [Management tasks for Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md).

## <a name="bkmk_winphone"></a> Create Windows Phone application

A Configuration Manager application has one or more deployment types. The deployment type includes the installation files and information that's required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.

For the general steps to create an app and deployment types, see [create an application](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager supports the following app file types For Windows mobile devices:

|Device type|Supported file types|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Deploy Windows Phone apps as **Available** or **Required**. Also use deployments to uninstall apps.

## Deploy and monitor apps

Deploy and monitor applications for mobile devices in Configuration Manager the same as you do for other devices, such as desktops and servers. For more information, see the following articles:

- [Deploy applications](../../apps/deploy-use/deploy-applications.md)
- [Monitor applications](../../apps/deploy-use/monitor-applications-from-the-console.md)

Review the following limitations specific to mobile devices:

- MDM-enrolled devices don't support simulated deployments, user experience, or scheduling settings.

- Don't add more than 100 locales to a single app. This action prevents the app from installing on the device.

## Next step

To make changes, uninstall, or replace a deployed application with a new application, manage it the same as any app in Configuration Manager. For more information, see [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md).
