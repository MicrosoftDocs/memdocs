---
# required metadata
title: Move a Cloud PC (preview) 
titleSuffix:
description: Learn how to move a Cloud PC by using Microsoft Intune.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/31/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Move a Cloud PC (preview)

By editing a provisioning policy, you can move an existing Cloud PC from its current region or Azure network connection (ANC) to a new one. You can move up to 100 Cloud PCs at a time.

When you start a Cloud PC move:

- All Cloud PCs in the provisioning policy that no longer match the updated region or ANC will be shutdown.
- All such Cloud PCs will be moved to the new region or ANC.
- It may take several hours for the moves to complete.

The best time to perform moves is over the weekend to make sure the impact to users is minimized. Also, you should notify your users before the move so that they can save their work and sign-off.

New Cloud PCs created by the edited provisioning policy are assigned to the new region or ANC.

Moving a Cloud PC  in [public preview](public-preview.md).

## Move a Cloud PC

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **Provisioning policies** > select a policy.
2. Under **General**, select **Edit**.
3. Under **Join type details**, make changes depending on the original type:
  
    - For **Hybrid Azure AD Join**, change the ANC\*.
    - For **Azure Active Directory (Azure AD) Join**:

      - You can change **Network** type from ANC to Microsoft hosted network, or vice versa.
      - If a **Microsoft hosted network** is used, change the **Geography** and/or **Region**.
      - If an **Azure network connection** is used, change the ANC\*.

4. Select **Next** > **Update**.
5. When ready to move the existing Cloud PCs, select **Apply region change to existing Cloud PCs**.

\* The domain defined in the new ANC must match that of the Cloud PCs that you want to move. The domain used in hte original ANC must be reachable from the new ANC.

All Cloud PCs provisioned after these changes are created in the new region.

## Move process

1. All Cloud PCs in the move are backed up before being moved to the new region. This backup, which can take some time, can begin while the user is signed in and active.
2. After the backup is complete, the Cloud PC is shut down.
3. The Cloud PC is moved. During this time, which can take several hours, the Cloud PC is inaccessible.

    - During the move, you can view the status in the **All Cloud PCs** list. The move is complete when the status indicates **Provisioned**.

4. After the move is complete, users can sign in.

If an error occurs, you retry the move.

<!-- ########################## -->
## Next steps

[Manage your Cloud PCs](device-management-overview.md).
