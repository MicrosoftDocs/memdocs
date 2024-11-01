---
# required metadata
title: Edit Azure network connections for Windows 365
titleSuffix:
description: Learn how to edit Azure network connections for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/30/2024
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

# Edit Azure network connection

All [Azure network connections](azure-network-connections.md) (ANC) get periodically checked to make sure that the environment is ready for provisioning Cloud PCs. If these [checks](health-checks.md) fail, you may need to fix your networking setup on Azure or edit one of the properties provided.

## Requirements

To edit  an ANC, you must have the [Intune Administrator](/azure/active-directory/roles/permissions-reference#intune-administrator) or [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference) role. You must also have the Subscription Reader role in the Azure Subscription where the VNET associated with the ANC was located.

## Edit an Azure network connection

To edit an Azure network connection:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**) > **Azure network connection** > select the connection you want to edit > **Properties**.
2. For all ANCs, you can edit the **General** settings by selecting **Edit** next to each header. You can edit all settings except **Join type**. For Microsoft Entra hybrid join connections, you can also edit the **AD domain** settings.

After the edits are saved, the ANC checks are run to verify the configuration.

You can't edit an ANC if it's running checks. You must wait for the checks to pass/fail before edit functionality becomes available.

Some configuration settings can't be edited for ANCs that are:

- Referenced by a provisioning policy, including as an alternate ANC.
- Used by a Cloud PC.
- Configured as backup ANCs for [cross region disaster recovery](cross-region-disaster-recovery.md).

<!-- ########################## -->
## Next steps

[Delete Azure network connection](delete-azure-network-connection.md).
