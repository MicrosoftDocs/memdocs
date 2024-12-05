---
# required metadata
title: Move a Cloud PC 
titleSuffix:
description: Learn how to move a Cloud PC by using Microsoft Intune.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/06/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

# Move a Cloud PC

By editing a provisioning policy, you can move some or all existing Cloud PCs in a policy from:

- One region to another single region.
- One Azure network connection (ANC) to another ANC.
- a Microsoft hosted network to an ANC and vice versa.

## Bulk move all Cloud PCs in a policy

[!INCLUDE [Move a Cloud PC first steps](../includes/move-cloud-pc-steps.md)]
6. In the **Apply this configuration to existing Cloud PCs** box, select **Region or Azure network connections for all devices** > **Apply**.

\* The domain defined in the new ANC must match that of the Cloud PCs that you want to move. The domain used in the original ANC must be reachable from the new ANC.

All Cloud PCs provisioned after these changes are created in the new region.

## Move a subset of Cloud PCs

[!INCLUDE [Move a Cloud PC first steps](../includes/move-cloud-pc-steps.md)]
6. In the **Apply this configuration to existing Cloud PCs** box, select **Region or Azure network connections for select devices (preview)** > **Apply**.
7. Under **Select devices (prevew)**, select the devices that you want to move. You can move up to 100 devices at a time.
8. Choose **Select** > **Continue**.

## Best practices

The best time to perform moves is over the weekend to make sure the impact to users is minimized. Cloud PCs are shut down and inaccessible for up to several hours during the move process. You should notify your users before the move so that they can save their work and sign out.

When moving many devices to a new region, start with a few non-essential Cloud PCs and check for success before moving the critical Cloud PCs.

You can track the status of moving Cloud PCs with the [Cloud PC actions report](report-cloud-pc-actions.md).

New Cloud PCs created by the edited provisioning policy are assigned to the new region or ANC.

## Other move operations

Cloud PCs can't be moved from one provisioning policy to another.

You can't move some Cloud PCs to one region and other Cloud PCs to another region in the same policy edit operation.

You can't move Cloud PCs from one virtual network or subnet to another using the edit provisioning policy method. To make VNet/subnet changes, create a new ANC with the updated vNet/subnet and then move the Cloud PCs to the new ANC.

<!-- ########################## -->
## Next steps

[Manage your Cloud PCs](device-management-overview.md).
