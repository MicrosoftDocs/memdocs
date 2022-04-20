---
# required metadata
title: Delete Azure network connections for Windows 365
titleSuffix:
description: Learn how to delete Azure network connections for Windows 365.
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

# Delete Azure network connection

Only an unassigned Azure network connection (ANC) can be deleted. If an ANC is in use by a provisioning policy, then you must do one of the following:

- Remove the ANC from all provisioning policies.
- Delete the ANC.

To delete an Azure network connection:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**) > **Azure network connection**.
![Screenshot of delete connection](./media/delete-azure-network-connection/delete-connection.png)
2. Select the ellipses (**…**) next to the connection you want to delete > **Delete**.
3. Select **Confirm** when asked to delete the connection.

<!-- ########################## -->
## Next steps

[Add device images](add-device-images.md).
