---
# required metadata
title: Create a manual Cloud PC restore point in Windows 365
titleSuffix:
description: Learn how to create a manual Cloud PC restore point in Windows 365.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 05/31/2023
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

# Create on-demand manual restore points for Cloud PCs

Cloud PC [restore points](restore-overview.md) can be manually created both singly and in bulk.

## Create a single manual restore point

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > select a device > **Restore points**.
1. Select **Create Restore Points** > **Yes**.

The new restore point will be created. It may take up to an hour or more for the new restore point to appear in the list of restore points. If a restore point already exists for this Cloud PC it will be overwritten by the new restore point. 

## Create multiple manual restore points in bulk

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Bulk Device Actions**.
![Screenshot of bulk device actions.](./media/restore-bulk/bulk-device-actions.png)
1. On the **Basics** page, select the following options:
    1. **OS**: Windows
    1. **Device action**: Create Cloud PC manual restore point
1. Select **Next**.
1. On the **Devices** page, choose **Select devices to include**.
1. In the **Select devices**, choose the Cloud PCs that you want to create manual restore points for > **Select** > **Next**.
1. On the **Review + create** page, confirm your choices > **Create**.

The new restore points will be created. It may take up to an hour or more for the new restore points to appear in the list of restore points. If any of the selected Cloud PCs already have a restore point, the existing restore points will be overwritten.

<!-- ########################## -->
## Next steps

- [Restore a single Cloud PC](restore-single-cloud-pc.md)
- [Bulk restore multiple Cloud PCs](restore-bulk.md)
