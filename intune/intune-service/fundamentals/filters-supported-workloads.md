---
title: Platforms and policy types supported by assignment filters
description: Learn which apps, compliance policies, and device configuration profiles and their platforms support assignment filters in Microsoft Intune.
author: MandiOhlinger
ms.author: mandia
ms.date: 01/26/2026
ms.topic: reference
ms.reviewer: mattcall
ms.collection:
- M365-identity-device-management
---

# List of platforms, policies, and app types supported by assignment filters in Microsoft Intune

[Assignment filters in Intune](filters.md) help you target policies to specific devices and apps based on criteria, like OS version or device properties. You can use filters when assigning apps, compliance policies, device configuration profiles, and app configuration policies to **managed devices** (devices enrolled in Intune) and **managed apps** (apps managed by Intune).

This article lists the app types, compliance policies, device configuration profiles, and app configuration policies that support assignment filters. It also lists the workloads that aren't supported.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Before you begin

- ✅: Supports assignment filters.
- ❌: Doesn't support assignment filters.
- N/A: Doesn't apply to the platform.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

## Supported app types for managed devices

You can use assignment filters for some common app policies on the following platforms. For a list of what's not supported on managed devices, go to [not supported](#not-supported-on-managed-devices) (in this article).

# [Windows](#tab/windows-apps)

### Windows

| App type | Supported |
| --- | --- |
| Store app | ✅ |
| Microsoft 365 apps | ✅ |
| Microsoft Edge version 77 and newer | ✅ |
| Microsoft Defender for Endpoint | N/A |
| Web link | ❌ |
| Windows web link | ✅ |
| Line-of-business apps | ✅ |
| Windows app (Win32) | ✅ |
| Microsoft Store for Business | ✅ |

# [Android](#tab/android-apps)

### Android Enterprise

| App type | Supported |
| --- | --- |
| Store app | N/A |
| Microsoft 365 apps | N/A |
| Microsoft Edge version 77 and newer | N/A |
| Microsoft Defender for Endpoint | N/A |
| Web link | N/A |
| Line-of-business apps | N/A |
| Android Enterprise system app  | ✅ |
| Managed Google Play store app | ✅ |
| Managed Google Play web link | ✅ |
| Managed Android line-of-business app | ✅ |

> [!NOTE]
> Assignment filters aren't supported on Android Enterprise personally-owned devices with work profile (BYOD) when used in "Available" app assignments. If users are targeted with an "Available" app intent, then the app continues to show as available to install from the Google managed play store. Any include or exclude filtering is ignored.

### Android device administrator

| App type | Supported |
| --- | --- |
| Store app | ✅ |
| Microsoft 365 apps | N/A |
| Microsoft Edge version 77 and newer | N/A |
| Microsoft Defender for Endpoint | N/A |
| Web link | ❌ |
| Line-of-business apps | ✅ |

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

# [Apple](#tab/apple-apps)

### iOS/iPadOS

| App type | Supported |
| --- | --- |
| Store app | ✅ |
| Microsoft 365 apps | N/A |
| Microsoft Edge version 77 and newer | N/A |
| Microsoft Defender for Endpoint | N/A |
| Web link | ❌ |
| iOS/iPadOS web clip | ✅ |
| Line-of-business apps | ✅ |
| iOS/iPadOS volume purchase program (VPP) app | ✅ |

### macOS

| App type | Supported |
| --- | --- |
| Store app | N/A |
| Microsoft 365 apps | ✅ |
| Microsoft Edge version 77 and newer | ✅ |
| Microsoft Defender for Endpoint | ✅ |
| Web link | ❌ |
| Line-of-business apps | ✅ |

---

## [App configuration policies](../apps/app-configuration-policies-overview.md)

- For **managed apps**, you can use assignment filters for app configuration policies on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

- For **managed devices**, you can use assignment filters for app configuration policies on the following platforms:

  - Android Enterprise
  - iOS/iPadOS

## [App protection policies](../apps/app-protection-policy.md)

- For **managed apps**, you can use assignment filters for app protection policies on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

- For **managed devices**, assignment filters aren't supported for app protection policies. For other features not supported on managed devices, go to [not supported](#not-supported-on-managed-devices) (in this article).

## Compliance policies

- For **managed apps**, assignment filters aren't supported for compliance policies.
- For **managed devices**, you can use assignment filters for all compliance policies on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

## Device configuration profiles and Endpoint security

- For **managed apps**, assignment filters aren't supported for device configuration profiles and endpoint security policies.

- On **managed devices**, you can use filters for some common device configuration policies on the platforms listed in the following tables. For a list of what's not supported, go to [not supported](#not-supported-on-managed-devices) (in this article).

> [!NOTE]
> Some profile types are only available for specific platforms. For example, the **Device features** profile type includes settings that are only available for iOS/iPadOS and macOS devices.
>
> For a list of all device configuration profiles, and the platforms they apply to, go to [Apply features and settings on your devices](../configuration/device-profiles.md).

# [Windows](#tab/windows-device-configuration)

### Windows

| Profile type | Supported |
| --- | --- |
| Update rings for Windows | ✅ |
| &nbsp; | &nbsp; |
| **Device configuration profile** | &nbsp; |
| Custom | ✅ |
| Derived credential | N/A |
| Delivery optimization | ✅ |
| Device restrictions | ✅ |
| Device Restrictions (Windows 10 Team) | ✅ |
| Device Features | N/A |
| Device Firmware Configuration Interface (DFCI) on Windows on supported UEFI | ✅ |
| Domain Join | ✅ |
| Edition upgrade and S mode switch | ✅ |
| Email | ✅ |
| Endpoint analytics Remediations scripts|✅ |
| Endpoint Protection | ✅ |
| Enrollment device platform restrictions | ✅ <br/> Support for a subset of filter properties including device `osVersion`, `operatingSystemSKU`, and `enrollmentProfileName` |
| Kiosk | ✅ |
| Network boundary | ✅ |
| PKCS certificate | ✅ |
| PKCS imported certificate | ✅ |
| SCEP certificate | ✅ |
| Secure assessment (Education) | ✅ |
| Settings catalog | ✅ |
| Shared multi-user device | ✅ |
| Trusted certificate | ✅ |
| VPN | ✅ |
| Wi-Fi | ✅ |
| Wired network | ❌ |
| Windows health monitoring | ✅ |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | ✅ <br/> **Account protection**, **Local user group membership**, and **Local admin password solution (Windows LAPS)** |
| Antivirus | ✅ |
| Attack surface reduction | ✅ <br/> Excludes **Web protection (Microsoft Edge Legacy)**, **Application control**, and **App and browser isolation** |
| Disk encryption | ✅ |
| Endpoint detection and response | ✅ |
| Endpoint Privilege Management (EPM) |✅ |
| Firewall | ✅ |
| Microsoft Defender for Endpoint (Windows Desktop) | ✅ |
| Security baselines | ❌ |

# [Android](#tab/android-device-configuration)

### Android Enterprise

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | ✅ |
| Derived credential | ✅ |
| Device restrictions | ✅ |
| Device Restrictions (Windows 10 Team) | N/A |
| Device Features | N/A |
| Email | ✅ |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | ❌ |
| OEMConfig | ✅ |
| PKCS certificate | ✅ |
| PKCS imported certificate | ✅ |
| SCEP certificate | ✅ |
| Settings catalog | N/A |
| Trusted certificate | ✅ |
| VPN | ✅ |
| Wi-Fi | ✅ |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | N/A |
| Antivirus | N/A |
| Attack surface reduction | N/A |
| Disk encryption | N/A |
| Endpoint detection and response | N/A |
| Firewall | N/A |
| Security baselines | N/A |

### Android (AOSP)

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Device restrictions | ✅ |
| PKCS certificate | ✅ |
| SCEP certificate | ✅ |
| Trusted certificate | ✅ |

### Android device administrator

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | ✅ |
| Derived credential | N/A |
| Device restrictions | ✅ |
| Device restrictions (Windows 10 Team) | N/A |
| Device features | N/A |
| Email | N/A |
| Email (Samsung KNOX only) | ✅ |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | ❌ |
| MX profile (Zebra only) | ✅ |
| PKCS certificate | ✅ |
| PKCS imported certificate | ✅ |
| SCEP certificate | ✅ |
| Settings catalog | N/A |
| Trusted certificate | ✅ |
| VPN | ✅ |
| Wi-Fi | ✅ |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | N/A |
| Antivirus | N/A |
| Attack surface reduction | N/A |
| Disk encryption | N/A |
| Endpoint detection and response | N/A |
| Firewall | N/A |
| Security baselines | N/A |

# [Apple](#tab/apple-device-configuration)

### iOS/iPadOS

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | ✅ |
| Derived credential | ✅ |
| Device restrictions | ✅ |
| Device Restrictions (Windows 10 Team) | N/A |
| Device Features | ✅ |
| Email | ✅ |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | ✅ |
| PKCS certificate | ✅ |
| PKCS imported certificate | ✅ |
| SCEP certificate | ✅ |
| Settings catalog (MDM) | ✅ |
| Settings catalog (DDM) | ✅ |
| Trusted certificate | ✅ |
| VPN | ✅ |
| Wi-Fi | ✅ |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | N/A |
| Antivirus | N/A |
| Attack surface reduction | N/A |
| Disk encryption | N/A |
| Endpoint detection and response | N/A |
| Firewall | N/A  |
| Security baselines | N/A |

### macOS

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | ✅ |
| Derived credential | N/A |
| Device restrictions | ✅ |
| Device restrictions (Windows 10 Team) | N/A |
| Device features | ✅ |
| Email | N/A |
| Endpoint Protection | ✅ |
| Enrollment device platform restrictions | ✅ |
| Extensions | ✅ |
| PKCS certificate | ✅ |
| PKCS imported certificate | ✅ |
| Preference file | ✅ |
| SCEP certificate | ✅ |
| Settings catalog (MDM) | ✅ |
| Settings catalog (DDM) | ✅ |
| Trusted certificate | ✅ |
| VPN | ✅ |
| Wi-Fi | ✅ |
| Wired network | ✅ |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | N/A |
| Antivirus | ❌ |
| Attack surface reduction | N/A |
| Disk encryption | ❌ |
| Endpoint detection and response | N/A |
| Firewall | ❌ |
| Security baselines | N/A |

---

## Not supported on managed devices

The following features on managed devices don't support using assignment filters:

- Custom compliance policies for Windows (preview)
- App protection policies for Android and iOS/iPadOS

  You can use assignment filters on app protection policies for managed apps. For more information on managed apps, go to [Use filters when assigning your apps, policies, and profiles in Intune](filters.md).

- End user experiences customization policies
- iOS/iPadOS app provisioning profiles
- Partner device management
- Policies for Office apps
- Policy sets
- PowerShell scripts for Windows
- S mode supplemental policies for Windows
- Shell scripts for macOS
- Terms and conditions
- Update policies for iOS/iPadOS
- Feature updates for Windows
- Enrollment notifications
- Linux platform workloads
- Devices that are targeted with Endpoint Security configuration using Microsoft Defender for Endpoint integration, such as servers. These devices aren't enrolled in Intune.

## Related content

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported device properties when creating assignment filters](filters-device-properties.md)
