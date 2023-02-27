---
# required metadata
title: Manage Windows 365 Cloud PCs with Configuration Manager
titleSuffix:
description: Learn how to manage Cloud PCs with Configuration Manager.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/02/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tanishi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Manage Windows 365 Cloud PCs with Configuration Manager

By default, Cloud PCs are managed by using Intune. However, you can also manage Cloud PCs using co-management with Configuration Manager. To use Configuration Manager, you’ll need to [install the Configuration Manager client](/mem/configmgr/comanage/how-to-prepare-win10#install-the-configuration-manager-client) and [enable co-management](/mem/configmgr/comanage/how-to-enable). Managing Cloud PCs with Configuration Manager is fundamentally the same process as using Autopilot with Co-management.

For more information about co-management and how to set it up, see [What is co-management?]( /mem/configmgr/comanage/overview)

## Requirements

To manage Cloud PCs by using Configuration Manager co-management, you must meet the following requirements:

- Make sure that each Cloud PC user has been assigned both a Cloud PC license and an Intune license. Cloud PC provisioning will fail if the user doesn’t have both licenses. The Enrollment Status Page (ESP) will also fail.
- [Enable co-management in Configuration Manager](/mem/configmgr/comanage/how-to-enable).
- Distribute the ccmsetup.msi installer as a Line-of-Business (LOB) client app from Microsoft Intune. For more information, see How to [Install the Configuration Manager client](/mem/configmgr/comanage/how-to-prepare-win10#install-the-configuration-manager-client).
- If deploying Hybrid Azure AD joined Cloud PCs: In Configuration Manager, disable Enable automatic site-wide client push installation. For more information, see [How to deploy clients to Windows computers in Configuration Manager](/mem/configmgr/core/clients/deploy/deploy-clients-to-windows-computers).

For an easier client application deployment, you can create an Azure AD group based on model type, using filters, or all devices of a Windows 365 provisioning profile.  For more information, see [Create a dynamic device group containing your Cloud PCs](./create-dynamic-device-group-all-cloudpcs.md).

## Co-management workloads for Windows 365 Cloud PCs

With few exceptions, Cloud PCs can be managed in the same way as physical PCs.  Some features of Configuration Manager don’t apply to Cloud PCs, like OSD and PXE.  

Administrators can control which service will manage which areas of Windows by toggling workloads. For more information, see [Co-management workloads](/mem/configmgr/comanage/workloads).

If you have a large number of applications to migrate to Microsoft Intune, consider directing end-users to the Company Portal. In the Company Portal, users can see applications assigned from both Configuration Manager and Microsoft Intune.

<!-- ########################## -->
## Next steps

For more information about co-management and how to set it up, see [What is co-management?]( /mem/configmgr/comanage/overview)
