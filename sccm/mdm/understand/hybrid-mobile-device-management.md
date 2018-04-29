---
title: "Hybrid mobile device management (MDM) with Microsoft Intune"
titleSuffix: "Configuration Manager"
description: "Learn about hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*


You can manage iOS, Windows, and Android devices with Configuration Manager and Microsoft Intune. All management tasks are handled from the Configuration Manager console where you perform the rest of your management tasks seamlessly integrated with Microsoft Intune's online service over the internet.  You can use Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned devices to access company data. Management capabilities on devices:

-   Retire and wipe devices
-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication
-   Deploy line-of-business (LOB) apps to devices
-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play
-   Collect hardware inventory
-   Collect software inventory by using built-in reports

To read about what new features are available for hybrid MDM, see [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md).

This document assumes that you are using Configuration Manager to manage computers, and that you are interested in extending the Configuration Manager console with Intune to manage mobile devices. To understand the differences between  Intune and hybrid mobile device management, see [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

After extending Configuration Manager with Intune, you can  enroll and manage corporate-owned devices or give users permission to enroll their personal devices. You can also manage company-owned devices with Intune using Configuration Manager.

## Hybrid MDM Enrollment
To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed.
- "Bring your own device" (BYOD) enrollment lets users enroll their personal phones, tablets, or PCs.
- Corporate-owned device (COD) enrollment enables management scenarios like remote wipe, shared devices, or user affinity for a device.
- If you use [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
