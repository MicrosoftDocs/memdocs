---
# required metadata
title: Overview of deploying Windows 365 Link devices
titleSuffix:
description: Learn how to deploy Windows 365 Link devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 Link deployment overview

Before users can use their Windows 365 Link to connect to their Cloud PC provided by their organization, admins must set up the organization's Microsoft Entra ID and Intune environments to manage, register, and enroll the device.

To set up your organization's environment to deploy and manage Windows 365 Link devices, admins must complete the following steps:

1. [Meet all requirements](requirements.md).
2. [Configure Microsoft Entra Device settings to let users join Windows 365 Link devices to Microsoft Entra](join-microsoft-entra.md).
3. [Configure Microsoft Entra Mobility settings to automatically enroll Windows 365 Link devices in Intune](intune-automatic-enrollment.md).
4. [Create an Intune filter for Windows 365 Link devices](create-intune-filter.md) (optional).
5. [Optimize enrollment restrictions to let Windows 365 Link devices enroll](enrollment-restrictions.md).
6. [Synchronize conditional access policies](conditional-access-policies-synchronize.md).
7. [Suppress single sign-on consent prompt](single-sign-on-suppress.md) (recommended).

After setting up deployment for your Windows 365 Link devices, you can start [onboarding](onboarding.md) them.

For more information about managing devices in microsoft Intune, see the [Microsoft Intune documentation](/mem/intune/fundamentals/what-is-intune).

<!-- ########################## -->
## Next steps

[Make sure your environment meets all requirements](requirements.md).
