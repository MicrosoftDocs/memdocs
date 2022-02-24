---
# required metadata
title: Overview of restoring a Cloud PC to a previous state
titleSuffix:
description: Learn about restoring a Cloud PC to a previous state.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 03/02/2022
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

# Point-in-time restore (preview)

Point-in-time restore lets an administrator restore a Cloud PC to an earlier point in time. Admins can also give users permission to restore their own Cloud PCs.

## Restore point options

You can choose to save restore points every 4, 6, 12, 16, or 24 hours. Each Cloud PC will have 10 restore points saved at the intervals that you define in the user setting. For example, if you chose  four hour intervals, a Cloud PC will have 10 restore points spread out every four hours over the last 40 hours.

As time passes and a new restore point is added, the oldest restore point is removed.

## Interim data is lost

All changes made to the Cloud PC between the saved restore point and when the restore is started will be lost. This lost information includes all data, applications, configurations, and other changes. External data stored in cloud services, like OneDrive, will behave as if a physical device were restored to restore point.

<!-- ########################## -->
## Next steps

To get started with the restore feature, you must first [configure a new or existing user setting](restore-configure.md) to give users the right permissions. After you’ve done that, admins can:

- [Restore a single Cloud PC](restore-single-cloud-pc.md) (users with permission can also restore their own Cloud PC)
- [Bulk restore multiple Cloud PCs](restore-bulk.md)
