---
title: "Device Enrollment Methods for hybrid MDM"
titleSuffix: "Configuration Manager"
description: "Device enrollment methods for hybrid MDM."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Overview of device enrollment methods

*Applies to: System Center Configuration Manager (Current Branch)*

After you extend Configuration Manager with Intune, you can enroll and manage corporate-owned devices or give users permission to enroll their personal devices. You can also manage company-owned devices with Intune using Configuration Manager.

The following table shows enrollment methods with their supported capabilities. These capabilities include:
- **Wipe** - Factory reset the device, removing all data. [Retire devices](../deploy-use/wipe-lock-reset-devices.md)
- **Affinity** - Associates devices with users. Required for mobile application management (MAM) and conditional access to company data. [User Affinity](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Lock** Prevents users from  removing the device from management. iOS devices require Supervised mode for Lock. [Remote lock](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**iOS enrollment methods**

| **Method** |	**Wipe** |	**Affinity**	|	**Lock** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|	Yes |	No | [more](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|	No |No |No	| [more](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|	Yes |	Optional |	Optional|[more](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**|	Yes |	Optional |	No| [more](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows and Android enrollment methods**

| **Method** |	**Wipe** |	**Affinity**	|	**Lock** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|	Yes |	No | [more](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|	No |No |No	|[more](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

For a series of question that help you find the right method, see [Choose how to enroll devices](/intune/get-started/choose-how-to-enroll-devices1).

## BYOD
"Bring your own device" (BYOD) users install the Company Portal app and enroll their device. This can let users connect to the company network, joining the domain or Azure Active Directory. Enabling BYOD enrollment is a prerequisite for many COD scenarios for most platforms. See [Setup hybrid MDM](../deploy-use/setup-hybrid-mdm.md). ([Back to the table](#overview-of-device-enrollment-methods))

## Corporate-owned devices
Corporate-owned devices (COD) can be managed with the Configuration Manager console. iOS devices can be enrolled directly through tools provided by Apple. All device types can be enrolled by an admin or manager using the device enrollment manager. Devices with an IMEI number can also be identified and tagged as company-owned to enable COD scenarios.

[Enroll corporate-owned devices](../deploy-use/enroll-company-owned-devices.md)

### DEM
Device enrollment manager is a special user account used to enroll and manage multiple corporate-owned devices. Managers can install the Company Portal and enroll many user-less devices. Learn more about [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Back to the table](#overview-of-device-enrollment-methods))

### DEP
Apple Device Enrollment Program (DEP) management lets you create and deploy policy “over the air” to iOS devices purchased and managed with DEP. The device is enrolled when the user turns on the device for the first time and runs the iOS Setup Assistant. This method supports **iOS Supervised** mode which in turn enables:
  -	Locked enrollment
  -	Conditional access
  -	Jailbreak detection
  -	Mobile application management

Learn more about [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Back to the table](#overview-of-device-enrollment-methods))

### USB-SA
USB-connected, Setup Assistant enrollment. The admin creates a policy and exports it to Apple Configurator. USB-connected, corporate-owned devices are prepared with policy. The admin must enroll each device by hand. Users receive their devices and run Setup Assistant, enrolling their device. This method supports **iOS Supervised** mode which in turn enables:
  -	Conditional access
  -	Jailbreak detection
  -	Mobile application management

Learn more about [Setup Assistant enrollment with Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Back to the table](#overview-of-device-enrollment-methods))

## Mobile device management with Exchange ActiveSync and Configuration Manager
Mobile devices that aren't enrolled but that connect to Exchange ActiveSync (EAS) can be managed by Intune using EAS MDM policy. Intune uses an Exchange Connector to communicate with EAS, either on-premises and cloud-hosted.

[Mobile device management with Exchange ActiveSync and Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
