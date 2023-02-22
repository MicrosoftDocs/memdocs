---
# required metadata
title: Reprovision a Cloud PC
titleSuffix:
description: Learn how to Reprovision a Cloud PC by using Microsoft Endpoint Manager.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
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

# Reprovision a Cloud PC

The **Reprovision** remote action deletes a user's current Cloud PC and creates a brand new Cloud PC for the same user.

When the **Reprovision** remote action starts, the user is signed off. The original Cloud PC is deleted, including all user data, applications, customizations, and so on.

To **Reprovision** a Cloud PC, it must have a status of **Failed** or **Provisioned** in the Windows 365 provisioning node.

For information on when to use the **Reprovision** action, see [Reprovisioning](provisioning.md#reprovisioning).

## Reprovision a Cloud PC

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All Devices** > choose a Cloud PC device > **Reprovision**.
![Screenshot of reprovision a Cloud PC](./media/reprovision-cloud-pc/reprovision.png)
2. In the **Reprovision** box, select **Yes**. The reprovision process will begin.
3. After the new Cloud PC is created, Windows 365 sends access information to the new user.

<!-- ########################## -->
## Next steps

For more information, see [Provisioning](provisioning.md).
