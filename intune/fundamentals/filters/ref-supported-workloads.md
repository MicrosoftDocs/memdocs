---
title: Platforms and policy types supported by assignment filters
description: Learn which apps, compliance policies, and device configuration profiles and their platforms support assignment filters in Microsoft Intune.
ms.date: 03/31/2026
ms.topic: reference
ms.reviewer: mattcall
ms.collection:
- M365-identity-device-management
---

# List of platforms, policies, and app types supported by assignment filters in Microsoft Intune

[Assignment filters in Intune](overview.md) help you target policies to specific devices and apps based on criteria, like OS version or device properties. You can use filters when assigning apps, compliance policies, device configuration profiles, and app configuration policies to **managed devices** (devices enrolled in Intune) and **managed apps** (apps managed by Intune).

This article lists the app types, compliance policies, device configuration profiles, and app configuration policies that support assignment filters. It also lists the workloads that aren't supported.

[!INCLUDE [android_device_administrator_support](../../includes/android-device-administrator-support.md)]

## Before you begin

- :::image type="icon" source="../../media/icons/16/check.svg" border="false":::: Supports assignment filters.
- :::image type="icon" source="../../media/icons/16/error.svg" border="false":::: Doesn't support assignment filters.
- N/A: Doesn't apply to the platform.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../../includes/windows-10-support.md)]

## Supported app types for managed devices

You can use assignment filters for some common app policies on the following platforms. For a list of what's not supported on managed devices, go to [not supported](#not-supported-on-managed-devices) (in this article).

# [Windows](#tab/windows-apps)

### Windows

| App type | Supported |
| --- | --- |
| Store app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft 365 apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Edge version 77 and newer | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Defender for Endpoint | N/A |
| Web link | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| Windows web link | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Line-of-business apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Windows app (Win32) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Store for Business | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

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
| Android Enterprise system app  | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Managed Google Play store app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Managed Google Play web link | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Managed Android line-of-business app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

> [!NOTE]
> Assignment filters aren't supported on Android Enterprise personally-owned devices with work profile (BYOD) when used in "Available" app assignments. If users are targeted with an "Available" app intent, then the app continues to show as available to install from the Google managed play store. Any include or exclude filtering is ignored.

### Android device administrator

| App type | Supported |
| --- | --- |
| Store app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft 365 apps | N/A |
| Microsoft Edge version 77 and newer | N/A |
| Microsoft Defender for Endpoint | N/A |
| Web link | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| Line-of-business apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

[!INCLUDE [android_device_administrator_support](../../includes/android-device-administrator-support.md)]

# [Apple](#tab/apple-apps)

### iOS/iPadOS

| App type | Supported |
| --- | --- |
| Store app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft 365 apps | N/A |
| Microsoft Edge version 77 and newer | N/A |
| Microsoft Defender for Endpoint | N/A |
| Web link | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| iOS/iPadOS web clip | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Line-of-business apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| iOS/iPadOS volume purchase program (VPP) app | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

### macOS

| App type | Supported |
| --- | --- |
| Store app | N/A |
| Microsoft 365 apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Edge version 77 and newer | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Defender for Endpoint | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Web link | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| Line-of-business apps | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

---

## [App configuration policies](../../app-management/configuration/overview.md)

- For **managed apps**, you can use assignment filters for app configuration policies on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

- For **managed devices**, you can use assignment filters for app configuration policies on the following platforms:

  - Android Enterprise
  - iOS/iPadOS

## [App protection policies](../../app-management/protection/overview.md)

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
> For a list of all device configuration profiles, and the platforms they apply to, go to [Apply features and settings on your devices](../../device-configuration/overview.md).

# [Windows](#tab/windows-device-configuration)

### Windows

| Profile type | Supported |
| --- | --- |
| Update rings for Windows | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| &nbsp; | &nbsp; |
| **Device configuration profile** | &nbsp; |
| Custom | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Derived credential | N/A |
| Delivery optimization | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device Restrictions (Windows 10 Team) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device Features | N/A |
| Device Firmware Configuration Interface (DFCI) on Windows on supported UEFI | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Domain Join | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Edition upgrade and S mode switch | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Email | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint analytics Remediations scripts|:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint Protection | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Enrollment device platform restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: <br/> Support for a subset of filter properties including device `osVersion`, `operatingSystemSKU`, and `enrollmentProfileName` |
| Kiosk | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Network boundary | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS imported certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Secure assessment (Education) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Shared multi-user device | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| VPN | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wi-Fi | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wired network | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| Windows health monitoring | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: <br/> **Account protection**, **Local user group membership**, and **Local admin password solution (Windows LAPS)** |
| Antivirus | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Attack surface reduction | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: <br/> Excludes **Web protection (Microsoft Edge Legacy)**, **Application control**, and **App and browser isolation** |
| Disk encryption | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint detection and response | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint Privilege Management (EPM) |:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Firewall | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Microsoft Defender for Endpoint (Windows Desktop) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Security baselines | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |

# [Android](#tab/android-device-configuration)

### Android Enterprise

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Derived credential | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device Restrictions (Windows 10 Team) | N/A |
| Device Features | N/A |
| Email | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| OEMConfig | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS imported certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog | N/A |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| VPN | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wi-Fi | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
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
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |

### Android device administrator

| Profile type | Supported |
| --- | --- |
| **Device configuration profile** | &nbsp; |
| Custom | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Derived credential | N/A |
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device restrictions (Windows 10 Team) | N/A |
| Device features | N/A |
| Email | N/A |
| Email (Samsung KNOX only) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | :::image type="icon" source="../../media/icons/16/error.svg" border="false"::: |
| MX profile (Zebra only) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS imported certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog | N/A |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| VPN | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wi-Fi | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
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
| Custom | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Derived credential | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device Restrictions (Windows 10 Team) | N/A |
| Device Features | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Email | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint Protection | N/A |
| Enrollment device platform restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS imported certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog (MDM) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog (DDM) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| VPN | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wi-Fi | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
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
| Custom | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Derived credential | N/A |
| Device restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Device restrictions (Windows 10 Team) | N/A |
| Device features | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Email | N/A |
| Endpoint Protection | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Enrollment device platform restrictions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Extensions | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| PKCS imported certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Preference file | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| SCEP certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog (MDM) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Settings catalog (DDM) | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Trusted certificate | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| VPN | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wi-Fi | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Wired network | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| &nbsp; | &nbsp; |
| **Endpoint Security profile** | &nbsp; |
| Account protection | N/A |
| Antivirus | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Attack surface reduction | N/A |
| Disk encryption | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Endpoint detection and response | N/A |
| Firewall | :::image type="icon" source="../../media/icons/16/check.svg" border="false"::: |
| Security baselines | N/A |

---

## Not supported on managed devices

The following features on managed devices don't support using assignment filters:

- Custom compliance policies for Windows (preview)
- App protection policies for Android and iOS/iPadOS

  You can use assignment filters on app protection policies for managed apps. For more information on managed apps, go to [Use filters when assigning your apps, policies, and profiles in Intune](overview.md).

- End user experiences customization policies
- Enrollment notifications
- Feature updates for Windows
- iOS/iPadOS app provisioning profiles
- Linux platform workloads
- Partner device management
- Policies for Office apps
- Policy sets
- PowerShell scripts for Windows
- S mode supplemental policies for Windows
- Shell scripts for macOS
- Terms and conditions
- Update policies MDM template for iOS/iPadOS (deprecated)
- Devices that are targeted with Endpoint Security configuration using Microsoft Defender for Endpoint integration, such as servers. These devices aren't enrolled in Intune.

## Related content

- [Use filters when assigning your apps, policies, and profiles](overview.md)
- [Supported device properties when creating assignment filters](ref-device-properties.md)
