---
# required metadata
title: Overview of deploying NXT devices
titleSuffix:
description: Learn how to deploy NXT devices
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

# NXT deployment overview

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

Before users can use their NXT to connect to their Cloud PC provided by your organization, admins must set up your Microsoft Entra and Intune environments to manage, register, and enroll the device.

To set up your organization's environment to deploy and manage NXT devices, admins must complete the following steps:

1. [Meet all requirements](requirements.md).
2. [Configure Microsoft Entra Device settings to let users join NXT devices to Microsoft Entra](join-microsoft-entra.md).
3. [Configure Microsoft Entra Mobility settings to automatically enroll NXT devices in Intune](intune-auotomatic-enrollment.md).
4. [Create an Intune filter for NXT devices](create-intune-filter.md).
5. [Optimize enrollment restrictions to let NXT devices enroll](enrollment-restrictions.md).
6. Synchronize conditional access policies.

<!-- ########################## -->
## Next steps

[Make sure your environment meets all requirements](requirements.md).
