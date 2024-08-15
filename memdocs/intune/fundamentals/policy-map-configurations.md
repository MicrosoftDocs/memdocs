---
# required metadata

title: Configurations policy mapping from Basic Mobility and Security to Intune
description: A detailed list of the policy map between Basic Mobility and Security configurations and Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/14/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Configurations policy mapping from Basic Mobility and Security to Intune

You can migrate from Basic Mobility and Security to Microsoft Intune. You can use the [Migration evaluation tool](migrate-to-intune.md) to automate much of this mapping.

After you migrate, use this article to map the settings in Microsoft Purview compliance portal configuration policies to the equivalent settings in Intune.

Intune offers more policy flexibility. So, each Office policy translates into multiple Intune and Microsoft Entra policies to achieve the same result.

To see these settings in the Microsoft Purview compliance portal, sign in to the [Purview compliance portal](https://protection.office.com/devicev2). Then, select **Device security policies** > policy name > **Edit policy** > **Configurations**.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Before you begin

- To configure the settings in an Intune policy, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md) lists and describes the built-in roles that can create policies.

## Require encrypted backup

This setting was never supported for Windows or Android in Basic Mobility and Security.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Compliance settings Edit** > **Cloud and Storage** > **Force encrypted backup**

## Block cloud backup

This setting was never supported for Windows or Android in Basic Mobility and Security.

This setting is only supported on supervices iOS devices.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **Cloud and Storage** > various **Block iCloud** settings

## Block document synchronization

This setting was never supported for Windows or Android in Basic Mobility and Security.

This setting is only supported on supervices iOS devices.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **Cloud and Storage** > **Block iCloud document and data sync**

## Block photo synchronization

This setting was never supported for Windows or Android in Basic Mobility and Security.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **Cloud and Storage** > **Block My Photo Stream**

## Block screen capture

For Android devices, this setting is only supported on Samsung Knox devices in Basic Mobility and Security.

Three Intune configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Screen capture (mobile only)**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Block screenshots and screen recording**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Screen capture (Samsung KNOX only)**

## Block video conferences on device

This setting was never supported for Windows or Android in Basic Mobility and Security.

This setting is only supported on supervised iOS devices.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **Built-in Apps** > **Block FaceTime**

## Block sending diagnostic data from device

For Android devices, this setting is only supported on Samsung Knox devices in Basic Mobility and Security.

For Windows 10 devices, the most restrictive value prevents sending security-related data.

Three Intune configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **Reporting and Telemetry** > **Share usage data**

  | Block sending diagnostic data from device value | Share usage data value |
  | --- | --- |
  | Selected | Security |
  | Not selected |  Not configured |

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Block sending diagnostic and usage data to Apple**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Diagnostic data (Samsung Knox only)**

## Block access to application store

For Android devices, this setting is only supported on Samsung Knox devices in Basic Mobility and Security.

For iOS, this setting is only supported on supervised iOS devices.

Three Intune configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **App store** > **App store (mobile only)**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **App store, Doc Viewing, Gaming** > **Block App store**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > choose a profile with type **Device administrator** > **Properties** > **Configuration settings Edit** > **Google Play Store** > **Google Play store (Samsung Knox only)**

## Require password when accessing application store

This setting was never supported for Windows or Android in Basic Mobility and Security.

Apple doesn't block accessing the app store without a password, but blocks purchases without a password.

One Intune configuration profile:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **App store, Doc Viewing, Gaming** > **Require iTunes Store password for all purchases**

## Block connection with removable storage

This setting was never supported for iOS/iPadOS in Basic Mobility and Security.

For Android devices, this setting is only supported on Samsung Knox devices in Basic Mobility and Security.

Two Intune configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Removable storage**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > choose a profile with type **Device administrator** > **Properties** > **Configuration settings Edit** > **Cloud and Storage** > **Removable storage (Samsung Knox only)**

## Block Bluetooth connection

This setting was never supported for iOS/iPadOS in Basic Mobility and Security.

For Android devices, this setting is only supported on Samsung Knox devices in Basic Mobility and Security.

Two Intune configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > profile name > **Properties** > **Configuration settings Edit** > > **Cellular and connectivity** > **Bluetooth**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > choose a profile with type **Device administrator** > **Properties** > **Configuration settings Edit** > **Cellular and connectivity** > **Bluetooth (Samsung Knox only)**

## Related article

To migrate these policies, you can use the [Migration evaluation tool](migrate-to-intune.md).
