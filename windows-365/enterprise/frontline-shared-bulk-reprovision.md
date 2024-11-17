---
# required metadata
title: Bulk reprovision Windows 365 Frontline Cloud PCs in shared mode
titleSuffix:
description: Learn how to bulk reprovision Windows 365 Frontline Cloud PCs in shared mode
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/19/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: gkomatsu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Bulk reprovision Windows 365 Frontline Cloud PCs in shared mode

Windows 365 Frontline Cloud PCs created in shared mode can be reprovisioned in bulk. Any data saved to individual Cloud PCs is removed.

Using bulk actions to reprovision multiple Cloud PCs at a time can help you:

- Apply new configurations. For example, apply a new image.
- Revert all Frontline Cloud PCs in shared mode to a known configuration. This can help minimize configuration discrepancies that might across your pool of available shared Cloud PCs. Such discrepancies might arise over time when different policies or updates are applied to individual systems.

## Bulk reprovision Windows 365 Fronline Cloud PCs in shared mode

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Device onboarding**) > **Provisioning policies**.
2. Select a provisioning policy for Frontline Cloud PCs.
3. Select **Reprovision**.
4. In the **Would you like to continue** > **Keep a percentage of devices available** box, type the percentage of the devices you want to keep available during the reprovisioning action.

    When choosing the percentage, consider the following:
      - Cloud PCs don't reprovision while users are still signed in. If you need to force users to be connected, start the reprovision, type 0%, then use the **Restart** remote action on each Cloud PC.
      - The minimum number of devices that will be reprovisioned is one. For example, if you have one Cloud PC and you specify 99%, the one device will still be reprovisioned, even though the closest whole number is one Cloud PC to be available.
      - The system rounds down to the nearest whole number. For example, if the total number of Cloud PCs is 150 and you keep 27% available, the result is 40.5 Cloud PCs. This is rounded down to keep 40 Cloud PCs available at a time.

<!-- ########################## -->
## Next steps

[Remotely manage Windows 365 Cloud PCs](remotely-manage-cloud-pc.md).
