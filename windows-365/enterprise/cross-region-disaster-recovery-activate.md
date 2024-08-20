---
# required metadata
title: Activate/deactivate cross regin disaster recovery in Windows 365.
titleSuffix:
description: Learn how to activate/deactivate cross regin disaster recovery in Windows 365.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: docoombs
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---
# Activate or deactive cross region disaster recovery in Windows 365

If there’s a regional outage, you must determine whether to activate [cross region disaster recovery](cross-region-disaster-recovery.md). Before doing so, you must [set up cross region disaster recovery](cross-region-disaster-recovery-set-up.md).

Using bulk actions, you can activate/deactivate cross region disaster recovery for individual devices or devices for all users in a group.

Activating cross region disaster recovery moves users to a new Cloud PC in a temporary region. Users can’t access their Cloud PCs until the move is complete. Until the cross region disaster recovery is deactivated, users work from a Cloud PC in this region.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** >**Bulk device actions**.
2. Check the [Cloud PCs cross region disaster recovery status]() report. If there are errors, work to correct them before continuing.
3. On the **Basics** page, select the following options:

    - **OS**: Windows
    - **Device type**: Cloud PCs
    - **Device action**: Cross region disaster recovery

4. For **Action type**, select one of the following options:
    - **Activate cross region disaster recovery**
    - **Deactivate cross region disaster recovery**. It may take up to one hour for the transfer back to the primary Cloud PC to complete. During this time, the user may continue to use their temporary backup Cloud PC. When the transfer completes, the user sign back into their primary device within a few minutes.

5. Select **Next**.
6. On the **Devices** page, select individual Cloud PCs or a group of Cloud PCs. When you select devices, only devices that are currently appropriate appear in the list. If you want to deactivate all devices that are currently Activated, you can select the box to select all devices.
7. Select **Next**.
8. On the **Review + create** page, select **Create**.

<!-- ########################## -->
## Next steps

Learn how to [set up](cross-region-disaster-recovery-set-up.md) and [monitor](cross-region-disaster-recovery-report.md) cross region disaster recovery.
