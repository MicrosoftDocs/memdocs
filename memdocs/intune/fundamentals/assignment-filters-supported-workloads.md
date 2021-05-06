---
# required metadata

title: Supported workloads for assignment filters in Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/04/2021
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

# Supported workloads

✔️: Supports filters.

❌: Doesn't support filters.


## Apps

You can use assignment filters for some common app configuration policies on the following platforms.

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

You can use assignment filters for all compliance policies on the following platforms:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

## Device configuration profiles and Endpoint security

You can use assignment filters for some common app configuration policies on the following platforms. Some profile types are only available for specific platforms. For example, the **Device features** profile type includes settings that are only available for iOS/iPadOS and macOS devices. The **OEMConfig** profile type includes settings that are only available for Android Enterprise devices.

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

- Android and iOS/iPadOS app configuration policies
- Android, iOS/iPadOS, and Windows 10 app protection policies
- iOS/iPadOS app provisioning profiles
- Customization policies ??
- Enrollment restriction policies
- iOS/iPadOS update policies
- Policies for Office apps ??App config policies? App protect policies?
- Policy sets
- Partner device management connectors ??
- Scripts for macOS and Windows 10 ??Powershell scripts?
- Terms and conditions
- Windows 10 S mode supplemental policies
- Windows 10 update rings
- Windows 10 feature updates

## Next steps
