---
# required metadata

title: Platforms and policy types supported by filters in Microsoft Intune - Azure | Microsoft Docs
description: Supported apps, compliance policies, and device configuration profiles that support filters in Microsoft Endpoint Manager and Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# List of platforms and policies supported by filters in Microsoft Endpoint Manager

When you create an app policy, compliance policy, or configuration profile, you assign the policy to users or devices. When you assign the policy, you can also use filters. For example, you can assign policies to Windows 10 devices running a specific OS version. For more information, see [Use filters when assigning your apps, policies, and profiles](filters.md).

Filters support some of the different workloads available in Microsoft Intune. This article lists the app types, compliance policies, and device configuration profiles that support filters. It also lists the workloads that aren't supported.

## Before you begin

- This article assume you're familiar with filters. If not, you can learn more at [Use filters when assigning your apps, policies, and profiles](filters.md).
- ✔️: Supports filters.
- ❌: Doesn't support filters.

## Apps

You can use filters for some common app policies on the following platforms. For a list of what's not supported, see [not supported](#not-supported) (in this article).

### Android device administrator

| App type | Supported |
| --- | --- |
| Store app | ✔️ |
| Microsoft 365 apps | ❌ |
| Microsoft Edge version 77 and newer | ❌ |
| Microsoft Defender for Endpoint | ❌ |
| Web link | ❌ |
| Line-of-business apps | ✔️ |

### Android Enterprise

| App type | Supported |
| --- | --- |
| Store app | ❌ |
| Microsoft 365 apps | ❌ |
| Microsoft Edge version 77 and newer | ❌ |
| Microsoft Defender for Endpoint | ❌ |
| Web link | ❌ |
| Line-of-business apps | ❌ |
| Android Enterprise system app  | ✔️ |
| Managed Google Play store app | ✔️ |
| Managed Google Play web link | ✔️ |
| Managed Android line-of-business app | ✔️ |

### iOS/iPadOS

| App type | Supported |
| --- | --- |
| Store app | ✔️ |
| Microsoft 365 apps | ❌ |
| Microsoft Edge version 77 and newer | ❌ |
| Microsoft Defender for Endpoint | ❌ |
| Web link | ❌ |
| Line-of-business apps | ✔️ |
| iOS/iPadOS volume purchase program (VPP) app | ✔️ |

### macOS

| App type | Supported |
| --- | --- |
| Store app | ❌ |
| Microsoft 365 apps | ✔️ |
| Microsoft Edge version 77 and newer | ✔️ |
| Microsoft Defender for Endpoint | ✔️ |
| Web link | ❌ |
| Line-of-business apps | ✔️ |

### Windows 10 and newer

| App type | Supported |
| --- | --- |
| Store app | ✔️ |
| Microsoft 365 apps | ✔️ |
| Microsoft Edge version 77 and newer | ✔️ |
| Microsoft Defender for Endpoint | ❌ |
| Web link | ❌ |
| Line-of-business apps | ✔️ |
| Windows app (Win32) | ✔️ |
| Microsoft Store for Business | ✔️ |

## Compliance policies

You can use filters for all compliance policies on the following platforms:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

## Device configuration profiles and Endpoint security

You can use filters for some common device configuration policies on the following platforms. For a list of what's not supported, see [not supported](#not-supported) (in this article).

Some profile types are only available for specific platforms. For example, the **Device features** profile type includes settings that are only available for iOS/iPadOS and macOS devices. The **OEMConfig** profile type includes settings that are only available for Android Enterprise devices.

### Android device administrator

| Profile type | Supported |
| --- | --- |
| Custom | ✔️ |
| Derived credential | ❌ |
| Device restrictions | ✔️ |
| Device restrictions (Windows 10 Team) | ❌ |
| Device features | ❌ |
| Email | ❌ |
| Email (Samsung KNOX only) | ✔️ |
| Endpoint Protection | ❌ |
| MX profile (Zebra only) | ✔️ |
| PKCS certificate | ✔️ |
| PKCS imported certificate | ✔️ |
| SCEP certificate | ✔️ |
| Settings catalog | ❌ |
| Trusted certificate | ✔️ |
| VPN | ✔️ |
| Wi-Fi | ✔️ |
| **Endpoint Security** | &nbsp; |
| Account protection | ❌ |
| Antivirus | ❌ |
| Attack surface reduction | ❌ |
| Disk encryption | ❌ |
| Endpoint detection and response | ❌ |
| Firewall | ❌ |
| Security Baselines | ❌ |

### Android Enterprise

| Profile type | Supported |
| --- | --- |
| Custom | ✔️ |
| Derived credential | ✔️ |
| Device restrictions | ✔️ |
| Device Restrictions (Windows 10 Team) | ❌ |
| Device Features | ❌ |
| Email | ✔️ |
| Endpoint Protection | ❌ |
| OEMConfig | ❌ |
| PKCS certificate | ✔️ |
| PKCS imported certificate | ✔️ |
| SCEP certificate | ✔️ |
| Settings catalog | ❌ |
| Trusted certificate | ✔️ |
| VPN | ✔️ |
| Wi-Fi | ✔️ |
| **Endpoint Security** | &nbsp; |
| Account protection | ❌ |
| Antivirus | ❌ |
| Attack surface reduction | ❌ |
| Disk encryption | ❌ |
| Endpoint detection and response | ❌ |
| Firewall | ❌ |
| Security Baselines | ❌ |

### iOS/iPadOS

| Profile type | Supported |
| --- | --- |
| Custom | ✔️ |
| Derived credential | ✔️ |
| Device restrictions | ✔️ |
| Device Restrictions (Windows 10 Team) | ❌ |
| Device Features | ✔️ |
| Email | ✔️ |
| Endpoint Protection | ❌ |
| PKCS certificate | ✔️ |
| PKCS imported certificate | ✔️ |
| SCEP certificate | ✔️ |
| Settings catalog | ❌ |
| Trusted certificate | ✔️ |
| VPN | ✔️ |
| Wi-Fi | ✔️ |
| **Endpoint Security** | &nbsp; |
| Account protection | ❌ |
| Antivirus | ❌ |
| Attack surface reduction | ❌ |
| Disk encryption | ❌ |
| Endpoint detection and response | ❌ |
| Firewall | ❌ |
| Security Baselines | ❌ |

### macOS

| Profile type | Supported |
| --- | --- |
| Custom | ✔️ |
| Derived credential | ❌ |
| Device restrictions | ✔️ |
| Device restrictions (Windows 10 Team) | ❌ |
| Device features | ✔️ |
| Email | ❌ |
| Endpoint Protection | ✔️ |
| Extensions | ✔️ |
| PKCS certificate | ✔️ |
| PKCS imported certificate | ✔️ |
| Preference file | ✔️ |
| SCEP certificate | ✔️ |
| Settings catalog | ✔️ |
| Trusted certificate | ✔️ |
| VPN | ✔️ |
| Wi-Fi | ✔️ |
| Wired network | ✔️ |
| **Endpoint Security** | &nbsp; |
| Account protection | ❌ |
| Antivirus | ❌ |
| Attack surface reduction | ❌ |
| Disk encryption | ❌ |
| Endpoint detection and response | ❌ |
| Firewall | ❌ |
| Security Baselines | ❌ |

### Windows 10 and newer

| Profile type | Supported |
| --- | --- |
| Administrative Templates | ✔️ |
| Custom | ✔️ |
| Derived credential | ❌ |
| Delivery optimization | ✔️ |
| Device restrictions | ✔️ |
| Device Restrictions (Windows 10 Team) | ✔️ |
| Device Features | ❌ |
| Device Firmware Configuration Interface | ❌ |
| Domain Join | ✔️ |
| Edition upgrade and S mode switch | ✔️ |
| Email | ✔️ |
| Endpoint Protection | ✔️ |
| Identity Protection | ✔️ |
| Kiosk | ✔️ |
| Microsoft Defender for Endpoint (Windows 10 Desktop) | ✔️ |
| Network boundary | ✔️ |
| PKCS certificate | ✔️ |
| PKCS imported certificate | ✔️ |
| SCEP certificate | ✔️ |
| Secure assessment (Education) | ✔️ |
| Settings catalog | ✔️ |
| Shared multi-user device | ✔️ |
| Trusted certificate | ✔️ |
| VPN | ✔️ |
| Wi-Fi | ✔️ |
| Windows health monitoring | ✔️ |
| **Endpoint Security** | &nbsp; |
| Account protection | ❌ |
| Antivirus | ❌ |
| Attack surface reduction | ❌ |
| Disk encryption | ❌ |
| Endpoint detection and response | ❌ |
| Firewall | ❌ |
| Security Baselines | ❌ |

## Not supported

The following features don't support using filters:

- App configuration policies for Android and iOS/iPadOS
- App protection policies for Android, iOS/iPadOS, and Windows 10
- iOS/iPadOS app provisioning profiles
- End user experiences customization policies
- Enrollment restrictions
- Policies for Office apps
- Policy sets
- Partner device management
- PowerShell scripts for Windows 10
- S mode supplemental policies for Windows 10
- Shell scripts for macOS
- Terms and conditions
- Update policies for iOS/iPadOS
- Windows 10 update rings
- Windows 10 feature updates

## Next steps

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported device properties when creating filters](filters-device-properties.md)
