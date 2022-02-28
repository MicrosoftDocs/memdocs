---
# required metadata
title: Overview of restoring a Cloud PC to a previous state
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

# Point-in-time restore (preview)

Point-in-time restore lets an administrator restore a Cloud PC to an earlier point in time. Admins can also give users permission to restore their own Cloud PCs.

## Restore point options

You can choose to save restore points every 4, 6, 12, 16, or 24 hours. Each Cloud PC will have 10 restore points saved at the intervals that you define in the user setting. For example, if you chose four hour intervals, a Cloud PC will have 10 restore points spread out every four hours over the last 40 hours.

As time passes and a new restore point is added, the oldest restore point is removed.

## Risks and results of restoring a Cloud PC

Cloud PCs have same risks as all Windows PCs when performing a full disk restore.  These risks and results include:

- All changes made to the Cloud PC between the saved restore point and when the restore is started will be lost. This lost information includes all data, documents, installed applications, configurations, downloads, and other changes. External data stored in cloud services, like OneDrive, won't be lost.
- The chances of data loss and [automated machine account password updates](known-issues-enterprise.md#restore-and-automatic-rolling-credentials) increase with longer time gaps between the selected restore point and the current time.

## Best practices

- To minimize data loss and the risk of a rolling password conflict, choose a restore point that is as close as possible to the current time.
- After a restoration is complete, the user should immediately sign into their Cloud PC to verify that they can successfully connect. If a user can't connect, or experiences unexpected behavior, try a second restoration to a different restore point that is more recent. On rare occasions you may need to reprovision/reset a Cloud PC if all restore points have obsolete rolling credentials.

<!-- ########################## -->
## Next steps

- To get started with the restore feature, you must first [configure a new or existing user setting](restore-configure.md) to give users the right permissions. After you’ve done that, admins can:
  - [Restore a single Cloud PC](restore-single-cloud-pc.md) (users with permission can also restore their own Cloud PC)
  - [Bulk restore multiple Cloud PCs](restore-bulk.md)
- Check [Known issues with restoring your Cloud PC](known-issues-enterprise.md)
