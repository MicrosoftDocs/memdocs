---
title: "Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune"
ms.custom: na
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

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
To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed. "Bring your own device" (BYOD) enrollment lets users enroll their personal phones, tablets, or PCs. Corporate-owned device (COD) enrollment enables management scenarios like remote wipe, shared devices, or user affinity for a device.

 If you use [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-intune), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](#manage-windows-pcs-with-intune).

## Overview of device enrollment methods

 The following table shows enrollment methods with their supported capabilities. These capabilities include:
 - **Wipe** - Factory reset the device, removing all data. [Retire devices](../deploy-use/rprotect-data-with-wipe-lock-or-passcode-reset.md)
 - **Affinity** - Associates devices with users. Required for mobile application management (MAM) and conditional access to company data. [User Affinity](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Lock** Prevents users from  removing the device from management. iOS devices require Supervised mode for Lock. [Remote lock](wipe-lock-reset-devices.md#block-access-a-device)

 **iOS enrollment methods**

| **Method** |	**Wipe** |	**Affinity**	|	**Lock** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|	Yes |	No | [more](../deploy-use/setup-hybrid-mdm#set-up-device-management)|
|**[DEM](#dem)**|	No |No |No	| [more](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|	Yes |	Optional |	Optional|[more](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**|	Yes |	Optional |	No| [more](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows and Android enrollment methods**

| **Method** |	**Wipe** |	**Affinity**	|	**Lock** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|	Yes |	No | [more](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[DEM](#dem)**|	No |No |No	|[more](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

For a series of question that help you find the right method, see [Choose how to enroll devices](/intune/get-started/choose-how-to-enroll-devices1).

## BYOD
"Bring your own device" users install the Company Portal app and enroll their device. This can let users connect to the company network, joining the domain or Azure Active Directory. Enabling BYOD enrollment is a prerequisite for many COD scenarios for most platforms. See [Prerequisites for device enrollment](../deploy-use/prerequisites-for-enrollment.md). ([Back to the table](#overview-of-device-enrollment-methods))

## Corporate-owned devices
Corporate-owned devices (COD) can be managed with the Configuration Manager console. iOS devices can be enrolled directly through tools provided by Apple. All device types can be enrolled by an admin or manager using the device enrollment manager. Devices with an IMEI number can also be identified and tagged as company-owned to enable COD scenarios.

[Enroll corporate-owned devices](enroll-company-owned-devices.md)

### DEM
Device enrollment manager is a special user account used to enroll and manage multiple corporate-owned devices. Managers can install the Company Portal and enroll many user-less devices. Learn more about [DEM](enroll-devices-with-device-enrollment-manager.md). ([Back to the table](#overview-of-device-enrollment-methods))

### DEP
Apple Device Enrollment Program (DEP) management lets you create and deploy policy “over the air” to iOS devices purchased and managed with DEP. The device is enrolled when the user turns on the device for the first time and runs the iOS Setup Assistant. This method supports **iOS Supervised** mode which in turn enables:
   -	Locked enrollment
   -	Conditional access
   -	Jailbreak detection
   -	Mobile application management

Learn more about [DEP](ios-device-enrollment-program-for-hybrid.md). ([Back to the table](#overview-of-device-enrollment-methods))

### USB-SA
USB-connected, Setup Assistant enrollment. The admin creates a policy and exports it to Apple Configurator. USB-connected, corporate-owned devices are prepared with policy. The admin must enroll each device by hand. Users receive their devices and run Setup Assistant, enrolling their device. This method supports **iOS Supervised** mode which in turn enables:
   -	Conditional access
   -	Jailbreak detection
   -	Mobile application management

Learn more about [Setup Assistant enrollment with Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md). ([Back to the table](#overview-of-device-enrollment-methods))

## Mobile device management with Exchange ActiveSync and Configuration Manager
Mobile devices that aren't enrolled but that connect to Exchange ActiveSync (EAS) can be managed by Intune using EAS MDM policy. Intune uses an Exchange Connector to communicate with EAS, either on-premises and cloud-hosted.

[Mobile device management with Exchange ActiveSync and Intune](manage-mobile-devices-with-exchange-activesync.md)


## Manage Windows PCs with Intune client software  
You can also manage Windows PCs using the Intune client software. PCs managed with the Intune client can:

  - Report software and hardware inventories
  - Install desktop applications (for example .exe and .msi files)
  - Firewall settings

PCs managed with the Intune client software cannot be wiped, and cannot take advantage of many Intune management features such as conditional access, VPN and Wi-Fi settings, or deployment of certificates and email configurations.

[Manage Windows PCs with Intune software client](../includes/manage-windows-pcs-with-microsoft-intune.md)

##  Supported device platforms

Configuration Manager hybrid MDM can manage the following device platforms:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## Next steps
 - [Prerequisites for device enrollment](prerequisites-for-enrollment.md)
 - [Manage corporate-owned devices](manage-corporate-owned-devices.md)
 - [Supported mobile  devices and computers](../get-started/supported-mobile-devices-and-computers.md)

