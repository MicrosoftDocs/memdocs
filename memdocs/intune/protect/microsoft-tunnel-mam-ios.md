---
title: Use Microsoft Tunnel VPN with iOS/iPad devices that don't enroll with Microsoft Intune
description: Add support for Mobile Application Management (MAM) for iOS to the Microsoft Tunnel Gateway. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/18/2023
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
ms.collection: M365-identity-device-management
---

# Microsoft Tunnel for Mobile Application Management for iOS/iPadOS (public preview)

In public preview, you can use Microsoft Tunnel VPN Gateway with unenrolled iOS devices to support Mobile Application Management (MAM) scenarios. With support for MAM, your unenrolled devices can use Tunnel to securely connect to your organization allowing users and apps safe access to your organizational data.

Applies to:  
- iOS/iPadOS

> [!NOTE]
> While in public preview, Microsoft Tunnel for MAM is available at no additional cost. When Tunnel for MAM becomes generally available, it will be available as a [**premium add-on**](/fundamentals/premium-add-ons.md) and require an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.


To extend your existing [Microsoft Tunnel configuration](../protect/microsoft-tunnel-configure.md) to support [MAM](../fundamentals/deployment-guide-enrollment-mamwe.md), you’ll create and deploy three profiles that configure this support on your unenrolled devices:






## Nex steps

- [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md)
- [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md)
- [MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
