---
# required metadata
title: Overview of restoring a Cloud PC to a previous state with Windows 365 Enterprise
titleSuffix:
description: Learn about restoring a Cloud PC to a previous state with Windows 365 Enterprise.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 03/06/2022
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Point-in-time restore for Windows 365 Enterprise

Point-in-time restore lets an administrator restore a Cloud PC to the exact state it was at an earlier point in time. You can [create new or edit settings](restore-configure.md) to automatically create restore points at regular intervals for groups of Cloud PCs. You can also create on-demand restore points for specific times. Admins can also give users permission to restore their own Cloud PCs.

## Restore point options

There are three different ways to to [set restore points](restore-configure.md):

- Short-term restore points
- Long-term restore points
- On-demand manual restore points

Each type of restore point can be [restored](restore-single-cloud-pc.md) in the same way.

### Short-term restore points

You can choose to set short-term restore points every 4, 6, 12, 16, or 24 hours. Each Cloud PC in the assigned groups will have 10 short-term restore points saved at the intervals that you define in the user setting. For example, if you chose four hour intervals, each assigned Cloud PC will have 10 restore points spread out every four hours over the last 40 hours.

### Long-term restore points

In addition to the configurable short-term restore points, there are also four long-term restore points that aren't configurable. These long-term restore points are saved every seven days.

### On-demand manual restore point

Manual restore points let administrators [create a restore point](create-manual-restore-point.md) whenever they want, for both a single a Cloud PC and groups of Cloud PCs (using bulk actions). Manual restore points are  in [public preview](../public-preview.md).

Among other uses, on-demand manual restore points are useful:

- For creating a backup before taking management actions.
- During employee off-boarding in conjunction with sharing a restore point.

Only administrators can create a manual restore point, and each Cloud PC can have only one manual restore point at a time.

### Expiration of restore points

For short- and long-term restore points, as time passes and a new restore point is added, the oldest restore point is removed.

Each Cloud PC can have one manual restore point. If you create another manual restore point for a Cloud PC that already has a manual restore point, the existing restore point will be overwritten by the new restore point. If not overwritten, a manual restore point expires in approximately 28 days. Manual restore points have an expiration date shown when they are created.

[!INCLUDE [Restore risks and best practices](../includes/restore-risks-best-practices.md)]

## Disaster recovery

When a restore is started, the virtual infrastructure used for the Cloud PC remains the same. If the infrastructure is unavailable, but appropriate alternate infrastructure is available in the same Azure region, then the Cloud PC is automatically placed in the available infrastructure. This makes sure that, in the case of a disaster recovery scenario in an Azure zone, that the Cloud PC is resilient through recovery to a different Zone in the region. The recovery to an alternate infrastructure is automatic. There is nothing required of the administrator or user other than to start the restore.

<!-- ########################## -->
## Next steps

- To get started with the short- and long-term restore points, you must first [configure point-in-time restore settings](restore-configure.md). After you’ve done that, admins can:
  - [Restore a single Cloud PC](restore-single-cloud-pc.md) (users with permission can also restore their own Cloud PC)
  - [Bulk restore multiple Cloud PCs](restore-bulk.md)
- [Create on-demand manual restore points](create-manual-restore-point.md).
- Check [Known issues with restoring your Cloud PC](known-issues-enterprise.md).
