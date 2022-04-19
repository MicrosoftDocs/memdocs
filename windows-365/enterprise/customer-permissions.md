---
# required metadata
title: Customer permissions needed for Windows 365 operations
titleSuffix:
description: Learn about customer permissions needed for some Windows 365 operations
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/05/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elaineyou
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Customer permissions

For some operations, Windows 365 needs permissions to other services. These operations include:

- Create an Azure network connection (ANC)
- Add a custom image

Windows 365 uses the Azure role-based access control (RBAC) permissions required for the corresponding operations.

## Create Azure network connections

You create OPNCs to define the connection between your network and the Windows 365 system so that Cloud PCs can be successfully provisioned. When you create an OPNC, the Windows 365 service requires the following permissions:

- **Reader permission on the Azure subscription**: This permission is used to simplify the flow when adding a custom image.
- **Network contributor on the specified resource group**: This permission is used to create network interface cards in the selected resource group.
- **Network contributor on the virtual network**: This permission is used to attach the created network interface cards to the selected virtual network. 

When you create an OPNC, you must be signed in with an account that is an Owner of the subscription.

For more information, see [Create Azure network connection](create-on-premises-network-connection.md).

## Add a custom image

If you’ve already created an OPNC for the image's associated Azure subscription, no new permissions are needed.

When you use a subscription without an OPNC, the Windows 365 service requires the following permission to upload a custom image:

- Reader of the subscription

When you upload a custom image, you must be signed in with an account that is an Owner or admin of the subscription.

For more information, see [Add or delete custom device images](add-device-images.md).

<!-- ########################## -->
## Next steps

[What is Azure role-based access control (Azure RBAC)](/azure/role-based-access-control/overview)?
