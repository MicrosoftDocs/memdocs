---
title: "Manage Applications"
titleSuffix: "Configuration Manager"
description: "Manage Applications in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---
# Manage Applications in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When you manage devices through Microsoft Intune or Configuration Manager on-premises device management, you can manage these additional application types:
- Windows Phone app package (*.xap file)
- App Package for iOS (*.ipa file)
- App Package for Android (*.apk file)
- App Package for Android on Google Play
- Windows Phone app package (in the Windows Phone Store)
- Windows Installer through MDM
- Web Application

This section provides detailed information about creating and managing applications using hybrid MDM or on-premises MDM.

[Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md) provides more general information about managing System Center Configuration Manager applications and deployment types.

## Deploying and monitoring apps

Deploying and monitoring applications in System Center Configuration Manager are the same processes for mobile devices as they are for onsite devices, such as laptops and desktops. You can read through the following topics for general information about deploying and monitoring applications:

- [Deploy applications in System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Monitor applications in System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Here are some considerations to keep in mind when deploying and monitoring applications, specific to mobile device management.

- MDM-enrolled devices do not support simulated deployments, user experience, or scheduling settings.

- You can associate the deployment with an iOS app configuration policy if you have already congured one. See [Configure iOS apps with app configuration policies](configure-ios-apps-with-app-configuration-policies.md).

### Next Steps

You might eventually want to make changes to an application, uninstall an application, or replace an already deployed application with a new application. Read through [Update and retire applications with System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) to understand these capabilities.
