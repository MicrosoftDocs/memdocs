---
# required metadata
title: Delete on-premises network connections for Windows 365
titleSuffix:
description: Learn how to delete on-premises network connections for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
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

# Delete on-premises network connection

Only a unassigned on-premises network connection (OPNC) can be deleted. If an OPNC is in use by a provisioning policy, then you must do one of the following:

- Remove the OPNC from all provisioning policies.
- Delete the OPNC.

To delete an on-premises network connection:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**) > **On-premises network connection**.
![Screenshot of delete connection](./media/delete-on-premises-network-connection/delete-connection.png)
2. Select the ellipses (**…**) next to the connection you want to delete > **Delete**.
3. Select **Confirm** when asked to delete the connection.

<!-- ########################## -->
## Next steps

[Add device images](add-device-images.md).
