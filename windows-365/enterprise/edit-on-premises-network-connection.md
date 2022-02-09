---
# required metadata
title: Edit on-premises network connections for Windows 365
titleSuffix:
description: Learn how to edit on-premises network connections for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/8/2022
ms.topic: how-to
ms.service: cloudpc
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
ms.collection: M365-identity-device-management
---

# Edit on-premises network connection

All [on-premises network connections](on-premises-network-connections.md) (OPNC) get periodically checked to make sure that the environment is ready for provisioning Cloud PCs. If these [checks](health-checks.md) fail, you may need to fix your networking setup on Azure or edit one of the properties provided.

To edit an on-premises network connection:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**) > **On-premises network connection** > select the connection you want to edit > **Properties**.
2. For all OPNCs, you can edit the **General** settings by selecting **Edit** next to each header. You can edit all settings except **Join type**. For Hybrid Azure AD Join connections, you can also edit the **AD domain** settings.

After the edits have been saved, the OPNC checks are run to verify the configuration.

You can't edit an OPNC if it's running checks. You must wait for the checks to pass/fail before edit functionality becomes available.

<!-- ########################## -->
## Next steps

[Delete on-premises network connection](delete-on-premises-network-connection.md).
