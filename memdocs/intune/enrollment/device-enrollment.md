---
# required metadata

title: What is Microsoft Intune device enrollment
titleSuffix: Microsoft Intune
description: Learn about enrollment for iOS/iPadOS, Android, and Windows devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/03/2021
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
  - M365-identity-device-management
  - highpri
---

# What is device enrollment in Intune?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune lets you manage your workforce's devices and apps and how they access your company data. To use this mobile device management (MDM), the devices must first be enrolled in the Intune service. When a device is enrolled, it's issued an MDM certificate. This certificate is used to communicate with the Intune service.

As you can see in the following tables, there are several methods to enroll your workforce's devices. Each method depends on the device's ownership (personal or corporate), device type (iOS, Windows, Android), and management requirements (resets, affinity, locking).

By default, devices for all platforms are allowed to enroll in Intune. However, you can [restrict devices by platform](enrollment-restrictions-set.md#create-a-device-platform-restriction) in Intune.

## iOS/iPadOS enrollment methods

| **Method** | **Reset required** | **User affinity** | **Locked** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
|Method used to enroll devices. |If yes, devices are wiped during enrollment. | If yes, each device is associated with a user.| If yes, users can't unenroll devices. |More information about method. |
|**[BYOD](#bring-your-own-device)** | No| Yes | No | [More information](apple-mdm-push-certificate-get.md)|
|**[DEM](#device-enrollment-manager)**| No |No |No | [More information](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Yes | Optional | Optional|[More information](device-enrollment-program-enroll-ios.md)|
|**[USB-SA](#usb-sa)**| Yes | Optional | No| [More information](apple-configurator-enroll-ios.md)|
|**[USB-Direct](#usb-direct)**| No | No | No|[More information](apple-configurator-enroll-ios.md)|

## macOS enrollment methods

| **Method** |  **Reset required** |  **User affinity** | **Locked** | **Details**|
|:---:|:---:|:---:|:---:|:---:|
|Method used to enroll devices. |If yes, devices are wiped during enrollment. | If yes, each device is associated with a user.| If yes, users can't unenroll devices. |More information about method.  |
|**[BYOD](#bring-your-own-device)** | No| Yes | No | [More information](macos-enroll.md)|
|**[DEM](#device-enrollment-manager)**| No |No |No  | [More information](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Yes | Optional | Optional|[More information](device-enrollment-program-enroll-macos.md)|

## Windows enrollment methods

| **Method** | **Reset required** | **User affinity** | **Locked** | **Details**|
|:---:|:---:|:---:|:---:|:---:|
|Method used to enroll devices. | If yes, devices are wiped during enrollment. | If yes, each device is associated with a user.| If yes, users can't unenroll devices. | More information about method. |
|**[BYOD](#bring-your-own-device)** | No | Yes | No | [More information](windows-enroll.md)|
|**[DEM](#device-enrollment-manager)**| No |No |No |[More information](device-enrollment-manager-enroll.md)|
|**Auto-enroll** | No |Yes |No | [More information](windows-enroll.md#enable-windows-automatic-enrollment)|
|**Autopilot** |Yes |Yes |No | [More information](../../autopilot/enrollment-autopilot.md)
|**Bulk enroll** |No |No |No | [More information](windows-bulk-enroll.md) |
|**Co-management** |No |Yes |No | [More information](/configmgr/core/clients/manage/co-management-overview)
|**GPO** |No |Yes |No | [More information](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)

## Android enrollment methods

### Personal enrollment methods

| **Enrollment type** | **Enrollment method** | **Reset required** | **User affinity** | **Locked** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|Name of enrollment type. |Method used to enroll devices.| If yes, devices are wiped during enrollment. | If yes, each device is associated with a user.| If yes, users can't unenroll devices. |More information about method. |
|**Android Device Admin**|**User initiated via Company Portal** | No | Yes | No | [More information](../user-help/enroll-device-android-company-portal.md)|
|**Android Enterprise personally-owned with Work Profile**|**User initiated via Company Portal**| No | Yes | No | [More information](android-work-profile-enroll.md)|

### Corporate enrollment methods

| **Enrollment type** | **Enrollment method** | **Reset required** | **User affinity** | **Locked** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|Name of enrollment type. |Method used to enroll devices.| If yes, devices are wiped during enrollment. | If yes, each device is associated with a user.| If yes, users can't unenroll devices. |More information about method. |
|**Android (AOSP) user-associated**|**QR code**|Yes|Yes|Configurable via policy|[More information](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)
|**Android (AOSP) userless**|**QR code**|Yes|No|Configurable via policy|[More information](../enrollment/android-aosp-corporate-owned-userless-enroll.md)
|**Android Device Admin**|**[DEM](#device-enrollment-manager) initiated via Company Portal**| No | No | No |[More information](device-enrollment-manager-enroll.md)|
|**Android Device Admin**|**(Pre-declared IMEI or SN) User initiated via Company Portal**| No | Yes | No | [More information](corporate-identifiers-add.md)|
|**Android Device Admin with Zebra Mobility Extensions**|**User or [DEM](#device-enrollment-manager) initiated via Company Portal**| No | Yes if user initiated, No if [DEM](#device-enrollment-manager) initiated | No | [More information](../configuration/android-zebra-mx-overview.md)|
|**Android Enterprise Dedicated**|**NFC, Token, QR code, Zero Touch**| Yes | No | Configurable via policy | [More information](android-kiosk-enroll.md)|
|**Android Enterprise Fully Managed**|**NFC, Token, QR code, Zero Touch**| Yes | Yes | Configurable via policy | [More information](android-dedicated-devices-fully-managed-enroll.md)|
|**Android Enterprise corporate-owned with Work Profile** | **NFC, Token, QR code, Zero Touch** | Yes | Yes | Configurable via policy | [More information](android-corporate-owned-work-profile-enroll.md)|

## Bring your own device

Bring your own devices (BYOD) include personally-owned phones, tablets, and PCs. Users install and run the Company Portal app to enroll BYODs. This program lets users access company resources like email.

## Corporate-owned device

[Corporate-owned devices (COD)](corporate-identifiers-add.md) include phones, tablets, and PCs owned by the organization and distributed to the workforce. COD enrollment supports scenarios like automatic enrollment, shared devices, or pre-authorized enrollment requirements. A common way to enroll CODs is for an administrator or manager to use the device enrollment manager (DEM). iOS/iPadOS devices can be enrolled directly through the ADE tools that are provided by Apple. Devices with an IMEI number can also be identified and tagged as corporate-owned.

### Device enrollment manager

Device enrollment manager (DEM) is a special user account that's used to enroll and manage multiple corporate-owned devices. Managers can install the Company Portal and enroll many user-less devices. These types of devices are good for point-of-sale or utility apps, for example, but not for users who need to access email or company resources. Learn more about [DEM](device-enrollment-manager-enroll.md).

### Apple Automated Device Enrollment

Apple Automated Device Enrollment (ADE) management lets you create and deploy policy "over the air" to iOS/iPadOS and macOS devices that are purchased and managed with ADE. The device is enrolled when users turn on the device for the first time and run Setup Assistant. This method supports iOS/iPadOS supervised mode, which enables a device to be configured with specific functionality.

Learn more about iOS/iPadOS ADE enrollment:

- [Choose how to enroll iOS/iPadOS devices](ios-enroll.md)
- [Enroll iOS/iPadOS devices using Device Enrollment Program](device-enrollment-program-enroll-ios.md)

### USB-SA

IT admins use Apple Configurator, through USB, to prepare each corporate-owned device manually for enrollment using Setup Assistant. The IT admin creates an enrollment profile and exports it to Apple Configurator. When users receive their devices, they're then prompted to run Setup Assistant to enroll their device. This method supports **iOS supervised** mode, which in turn enables the following features:

- Locked enrollment
- Kiosk mode and other advanced configurations and restrictions

Learn more about iOS/iPadOS Apple Configurator enrollment with Setup Assistant:

- [Decide how to enroll iOS/iPadOS devices](ios-enroll.md)
- [Enroll iOS/iPadOS devices with Configurator and Setup Assistant](apple-configurator-enroll-ios.md)

### USB-Direct
For direct enrollment, the admin must enroll each device manually by creating an enrollment policy and exporting it to Apple Configurator. USB-connected, corporate-owned devices are enrolled directly and don't require a wipe. Devices are managed as user-less devices. They're not locked or supervised and can't support Conditional Access, jailbreak detection, or mobile application management.

To learn more about iOS/iPadOS enrollment, see:

- [Decide how to enroll iOS/iPadOS devices](ios-enroll.md)
- [Enroll iOS/iPadOS devices with Configurator and direct enrollment](apple-configurator-enroll-ios.md)

## Mobile device cleanup after MDM certificate expiration

The MDM certificate is renewed automatically when mobile devices are communicating with the Intune service. If mobile devices are wiped, or they fail to communicate with the Intune service for some period of time, the MDM certificate isn't renewed. The device is removed from the Azure portal 180 days after the MDM certificate expires.
