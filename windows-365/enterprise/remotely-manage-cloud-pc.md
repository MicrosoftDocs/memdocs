---
# required metadata
title: Remotely manage Windows 365 devices
titleSuffix:
description: Learn how to remotely manage Windows 365 devices
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/07/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Remotely manage Windows 365 devices

You can remotely manage Cloud PCs in Intune just like any other managed device. For more information, see [Remotely run device actions with Intune](/mem/intune/remote-actions/).

Cloud PCs support the following remote management actions:

- Restart
- Sync
- Rename
- Quick Scan
- Full Scan
- Update Windows Defender
- [Reprovisioning](provisioning.md#reprovisioning) (this is a remote action specific to Cloud PC devices)
- [Resize](resize-cloud-pc.md#resize-a-cloud-pc) (this is a remote action specific to Cloud PC devices)
- [Collect diagnostics](/mem/intune/remote-actions/collect-diagnostics)

<!-- ########################## -->
## Next steps

[Reprovision a Cloud PC](reprovision-cloud-pc.md).
