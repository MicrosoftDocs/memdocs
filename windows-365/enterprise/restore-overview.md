---
# required metadata
title: Overview of restoring a Cloud PC to a previous state with Windows 365 Enterprise
titleSuffix:
description: Learn about restoring a Cloud PC to a previous state with Windows 365 Enterprise.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 10/25/2022
ms.topic: conceptual
ms.service: windows-365
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

# Point-in-time restore for Windows 365 Enterprise

Point-in-time restore lets an administrator restore a Cloud PC to the exact state it was at an earlier point in time. Admins can also give users permission to restore their own Cloud PCs.

## Restore point options

You can choose to save user-defined restore points every 4, 6, 12, 16, or 24 hours. Each Cloud PC will have 10 restore points saved at the intervals that you define in the user setting. For example, if you chose four hour intervals, a Cloud PC will have 10 restore points spread out every four hours over the last 40 hours.

In addition to these configurable short-term restore points, there are also default restore points taken every twelve hours that aren't configurable. These default restore points are saved for seven days for a total of 13 default restore points.

As time passes and a new restore point is added, the oldest restore point is removed.

[!INCLUDE [Restore risks and best practices](../includes/restore-risks-best-practices.md)]

## Disaster recovery

When a restore is started, the virtual infrastructure used for the Cloud PC remains the same. If the infrastructure is unavailable, but appropriate alternate infrastructure is available in the same Azure region, then the Cloud PC is automatically placed in the available infrastructure. This makes sure that, in the case of a disaster recovery scenario in an Azure zone, that the Cloud PC is resilient through recovery to a different Zone in the region. The recovery to an alternate infrastructure is automatic. There is nothing required of the administrator or user other than to start the restore.

<!-- ########################## -->
## Next steps

- To get started with the restore feature, you must first [configure a new or existing user setting](restore-configure.md) to give users the right permissions. After you’ve done that, admins can:
  - [Restore a single Cloud PC](restore-single-cloud-pc.md) (users with permission can also restore their own Cloud PC)
  - [Bulk restore multiple Cloud PCs](restore-bulk.md)
- Check [Known issues with restoring your Cloud PC](known-issues-enterprise.md)
