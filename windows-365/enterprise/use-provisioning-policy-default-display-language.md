---
# required metadata
title: Use a provisioning policy to set up a default display language on Cloud PCs
titleSuffix:
description: Learn how to provide a localized Windows experience for your Cloud PC users by using provisioning policies.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/25/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Use a provisioning policy to set up a default display language on Cloud PCs

To make sure that the correct language packs are available on the Cloud PC at first sign-in, you can configure a provisioning policy:

- [Create a provisioning policy](create-provisioning-policy.md) and choose a **Language & Region** under **Configuration**. There are 38 Windows language packs available for Windows 365. Windows 365 will automatically use the default remote keyboard layout for the language pack.

All Cloud PCs provisioned with this policy will have the chosen language pack at the first sign-in experience.

You can also [edit provisioning policies](edit-provisioning-policy.md) to change the Language & Region configuration. After you save the policy and [reprovision](reprovision-cloud-pc.md) the associated Cloud PCs, the chosen language pack will be on the Cloud PCs.

## Next steps

[Required URLs for language packs](provide-localized-windows-experience.md)
