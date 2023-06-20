---
# required metadata
title: Resize a Cloud PC (preview) 
titleSuffix:
description: Learn how to resize a Cloud PC by using Microsoft Endpoint Manager.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/30/2022
ms.topic: overview
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Resize a Cloud PC (preview)

The **Resize** remote action lets you upgrade a Windows 365 Enterprise Cloud PC’s RAM, vCPU, and storage size to meet the user’s needs. Resizing is important for users that need to:

- Upgrade a Windows 365 Enterprise Cloud PC’s RAM, vCPU, and storage size to meet the user’s needs.
- Downgrade the RAM and vCPU of a Cloud PC.

Resizing gives admins the flexibility to upgrade/downgrade the following specifications without having to provision Cloud PCs from scratch:

- Increase the RAM and vCPUs when a user requires CPU intensive applications.
- Increase the disk space for file storing.
- Decrease the RAM and vCPUs when a user doesn't need to run CPU intensive applications.

Resizing doesn't let you downsize disk space.

Resizing preserves user data. Users will be able to access all of their data after the resizing is finished.

## Requirements

To resize a Cloud PC, the admin must have any of the following built in Azure Active Directory (Azure AD) roles:

- Global Admin
- Intune Service Admin
- Intune Reader + Cloud PC Admin roles

Alternatively, you can assign a custom role that includes the permissions of these built-in roles.

In order to use **Resize** there should be a license of the appropriate target SKU available that isn't assigned to any user.

To **Resize** a Cloud PC, it must have a status of **Provisioned** in the Windows 365 provisioning node

The **Resize** remote action is supported for paid, preview, and trial licenses.

Resizing isn’t supported for Cloud PCs provisioned through group-based licenses.

Downsizing may impact support for nested virtualization. For more information, see [Set up virtualization-based workloads support](nested-virtualization.md).

## Resize a Cloud PC

1. Contact your end users and have them save their work and sign out. Resizing automatically disconnects the user from their session and any unsaved work might be lost. Therefore, it's best to coordinate any resizing with the user before you begin.
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All Devices** > choose a device > **Resize**.
![Screenshot of resize a Cloud PC](./media/resize-cloud-pc/resize.png)
3. You’ll see a list with all the possible SKUs that you can upgrade to. You increase and decrease a Cloud PC’s specs (RAM/vCPU). You can only increase the OS disk storage. You can't decrease the OS disk storage. If you're downsizing a user’s Cloud PC, options with lower storage will be grayed out. Select one of the available options.
4. Select **Resize**.
    - When you trigger a resize, the Cloud PC is rebooted and the user is immediately disconnected from their current session. Make sure the user saves all their work to avoid any potential data loss.
    - If there are available licenses, the upgrade/downgrade will take place.
    - If you have a combination of paid and trial licenses, the resize feature uses your paid licenses first. After these licenses run out, the resize operation uses your trial licenses.
    - If there are no licenses in your inventory, the resizing will fail. You can contact your procurement admin to request more licenses. After the license has been purchased and added to the inventory in the Microsoft Admin Center, you can retry the resize operation.

<!-- ########################## -->
## Next steps

For more information on Cloud PC sizes, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).
