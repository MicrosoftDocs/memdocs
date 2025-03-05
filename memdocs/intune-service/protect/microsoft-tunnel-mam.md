---
title: Learn about using Microsoft Tunnel with Mobile Application Management
description: Use Microsoft Tunnel for MAM with Android and iOS devices. Tunnel for MAM expands access to your organizational resources for devices that aren't or can't enroll with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/10/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-intune-suite
---

# Microsoft Tunnel for Mobile Application Management

[!INCLUDE [intune-add-on-note](../includes/intune-plan2-suite-note.md)]

When you use the Microsoft Tunnel VPN Gateway, you can extend Tunnel support by adding Tunnel for Mobile Application Management (MAM). Tunnel for MAM extends the Microsoft Tunnel VPN gateway to support devices that run Android or iOS, and that aren't enrolled with Microsoft Intune. With this solution, your users can use a single device that isn't enrolled with Intune to gain secure access to the organizations on-premises apps and resources using modern authentication, single sign-on, and Conditional Access. With Tunnel for MAM, your users can use their own device (BYOD) for both work and personal use, without having to grant the organization's IT department control over that device.

Applies to:

- Android
- iOS/iPadOS

## Platform requirements and feature overview

Before you begin, you must already have deployed the Microsoft Tunnel gateway. To learn more about Microsoft Tunnel gateway and how to install and configure it, see:

- [Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)
- [Identify the prerequisites to install and use the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-prerequisites.md)
- [Install and configure Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-configure.md)

Microsoft Tunnel for MAM supports the following platforms:

- Android Enterprise version 10.0 or higher
- iOS version 14.0 or higher

The following table identifies key features for the supported platforms:

| Requirements and Features        |Tunnel for Android     | Tunnel for iOS           |
|------------------|-----------------------|--------------------------|
| Requirements:    | - Company Portal app (sign-in not required)</br></br> - Defender for Endpoint app     | - No Company Portal app or Defender for Endpoint app requirement   |
| Features:        | - VPN is provided via the Defender for Endpoint app: </br> --- Per App VPN </br> --- Device-wide VPN </br></br> - *Auto-launch*: VPN automatically starts on app launch   | - VPN is provided via Tunnel for MAM SDK for iOS integration </br></br> - Per-App VPN. Tunnel connection is restricted to each targeted app </br></br> - *Auto-launch*: VPN automatically starts on app launch </br></br>   -  No Device-wide VPN </br></br> - Trusted root certificate support for on-premises CA trust </br></br>  |
| Line of Business app requirements| - Intune App SDK for Android </br></br> - Microsoft Authentication Library (MSAL) integration  | - Intune App SDK for iOS  </br></br> - Microsoft Authentication Library (MSAL) integration </br> --- Microsoft Entra App registration </br></br> - Tunnel for MAM SDK for iOS    |
| Microsoft Edge browser support:| - *Strict Tunnel Mode*: When users sign into Microsoft Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again. </br></br> - *Identity switch*: VPN connects when using a work or school account and disconnects when switching to a personal account or in-Private browsing. </br></br> - Device-wide and Per-App VPN support  | - *Strict Tunnel Mode*: When users sign into Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again. </br></br> - *Identity switch*: VPN connects when using a work/school account and disconnects when switching to a personal account or in-Private browsing.   |
| Third-party browser support:     | - Only with device-wide VPN enabled  | - None  |

## Try the interactive demos

Try the following interactive demos to discover how Tunnel for MAM extends Microsoft Tunnel VPN Gateway to support Android and iOS devices that aren't enrolled with Intune.

- [Microsoft Tunnel for Mobile Application Management for Android]( https://regale.cloud/Microsoft/viewer/1896/microsoft-tunnel-for-mobile-application-management-for-android/index.html#/0/0)
- [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS]( https://regale.cloud/Microsoft/viewer/1976/microsoft-tunnel-for-mobile-application-management-for-ios-ipados/index.html#/0/0)

## Related content

- [Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)
- [Use MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
- [MAM Tunnel for iOS](../protect/microsoft-tunnel-mam-ios.md)
