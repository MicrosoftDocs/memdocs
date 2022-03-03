---
# required metadata
title: Overview of restoring a Cloud PC to a previous state with Windows 365 Business
titleSuffix:
description: Learn about restoring a Cloud PC to a previous state.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 03/03/2022
ms.topic: conceptual
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: docoombs
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Point-in-time restore for Windows 365 Business (preview)

Point-in-time restore lets end users restore a Cloud PC to the exact state it was at an earlier point in time.

## Restore point intervals

Short-term restore points are saved every 12 hours. Each Cloud PC will have 10 short-term restore points saved at these intervals.

In addition to these short-term restore points, there are also four long-term restore points. These long-term restore points are saved every seven days.

As time passes and a new short-term or long-term restore point is added, the oldest short-term/long-term (respectively) restore point is removed.

[!INCLUDE [Restore risks and best practices](../includes/restore-risks-best-practices.md)]

## End user interface

To restore their Cloud PC, an end user must sign in to https://windows365.microsoft.com, select the gear icon, select **Restore (preview)**, and follow the onscreen prompts.

<!-- ########################## -->
## Next steps

[Manage your Cloud PCs](device-management.md)
