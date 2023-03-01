---
title: Learn about using Microsoft Tunnel with Mobile Application Management
description: Use Microsoft Tunnel for MAM with Android and iOS devices. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/01/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

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
---

# Microsoft Tunnel for Mobile Application Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

When you use the Microsoft Tunnel VPN Gateway, you can extend Tunnel support by adding Tunnel for Mobile Application Management (MAM). Tunnel for MAM extends the Microsoft Tunnel VPN gateway to support devices that run Android or iOS, and that aren't enrolled with Microsoft Intune. With this solution, your users can use a single device that hasn't enrolled with Intune to gain secure access to the organizations on-premises apps and resources using modern authentication, Single Sign On and conditional access. With Tunnel for MAM, your users can use their own device (BYOD) for both work and personal use, without having to grant the organization’s IT department control over that device.

Applies to:

<<<<<<< HEAD
- Android  (In public preview)
- iOS/iPadOS (In public preview)

> [!NOTE]
> While in public preview, Microsoft Tunnel for MAM is available at no additional cost. When Tunnel for MAM becomes generally available, it will be available as a [**Intune add-on**](../fundamentals/intune-add-ons.md) and require an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.
=======
- Android
- iOS/iPadOS
>>>>>>> ec15274579975ba52dc3cb0b93de4b87bd4359a0

## Platform requirements and feature overview

Before you begin, you must already have deployed the Microsoft Tunnel gateway. To learn more about Microsoft Tunnel gateway and how to install and configure it,  see:

- [Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)
- [Identify the prerequisites to install and use the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-prerequisites.md)
- [Install and configure Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-configure.md)

Microsoft Tunnel for MAM supports the following platforms:

- Android Enterprise version 10.0 or higher
- iOS version 14.0 or higher

The following table identifies key features for the supported platforms:

| Requirements and Features        |Tunnel for Android     | Tunnel for iOS           |
|------------------|-----------------------|--------------------------|
| Requirements:    | - Company Portal app (sign-in not required)<br><br> - Defender for Endpoint app     | - No Company Portal app or Defender for Endpoint app requirement   |
| Features:        | - VPN is provided via the Defender for Endpoint app: <br> --- Per App VPN <br> --- Device-wide VPN <br><br> - *Auto-launch*: VPN automatically starts on app launch   | - VPN is provided via Tunnel for MAM SDK for iOS integration <br><br> - Per-App VPN. Tunnel connection is restricted to each targeted app <br><br> - *Auto-launch*: VPN automatically starts on app launch <br><br>   -  No Device-wide VPN <br><br> - Trusted root certificate support for on-premises CA trust <br><br>  |
| Line of Business app requirements| - Intune App SDK for Android <br><br> - Microsoft Authentication Library (MSAL) integration  | - Intune App SDK for iOS  <br><br> - Microsoft Authentication Library (MSAL) integration <br> --- Azure AD App registration <br><br> - Tunnel for MAM SDK for iOS    |
| Microsoft Edge browser support:| - *Identity switch*: VPN connects when using a work or school account and disconnects when switching to a personal account or in-Private browsing <br><br> - Device-wide and Per-App VPN support  | - *Identity switch*: VPN connects when using a work/school account and disconnects when switching to a personal account or in-Private browsing   |
| Third-party browser support:     | - Only with device-wide VPN enabled  | - None  |

## Next steps

- [Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)
- [Use MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
- [MAM Tunnel for iOS](../protect/microsoft-tunnel-mam-ios.md)