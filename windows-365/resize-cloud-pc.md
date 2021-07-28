---
# required metadata
title: Resize a Cloud PC
titleSuffix:
description: Learn how to resize a Cloud PC by using Microsoft Endpoint Manager.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 7/26/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Resize a Cloud PC

The **Resize** remote action lets you upgrade a Cloud PC’s RAM, CPU, and storage size to meet the user’s needs. This is important for users that need more powerful Cloud PCs to run CPU intensive applications, or for users that need more disk space for file storing.

## Requirements

To resize a Cloud PC, the admin must have any of the following built in Azure Active Directory roles:

- Global Admin
- Intune Service Admin
- Windows 365 Service Admin  
- Cloud PC Admin  

Alternatively, you can assign a custom role that includes the permissions of the built in roles above.

To **Resize** a Cloud PC, it must have a status of **Provisioned** in the Windows 365 provisioning node

Resizing isn’t supported for group-based licenses.

## Resize a Cloud PC

1. Contact your end users and have them save their work and sign out. Resizing automatically disconnects the user from their session and any unsaved work might be lost. Therefore, it's best to coordinate any resizing with the user before you begin.
2. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All Devices** > choose a device > **Resize**.
![Screenshot of resize a Cloud PC](./media/resize-cloud-pc/resize.png)
3. You’ll see a list with all the possible SKUs that you can upgrade to. You can only increase a Cloud PC’s storage and specifications. Options with lower storage or specifications are grayed out. Select one of the available options.
4. Select **Resize**.
    - If there are available licenses the upgrade will take place.
    - If there are no licenses in your inventory, the resizing will fail. You can contact your procurement admin to request more licenses. After the license has been purchased and added to the inventory in the Microsoft Admin Center, you can retry the resize operation.

<!-- ########################## -->
## Next steps
For more information on Cloud PC sizes, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).
