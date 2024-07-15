---
title: Admins deploying apps to Windows 365 Business Cloud PCs
description: Learn about admins deploying apps to Windows 365 Business Cloud PCs.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 10/18/2023
audience: Admin
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier1
- essentials-manage
---

# Set up Intune so admins can deploy apps to Cloud PCs

Admins can deploy apps to users' Cloud PCs by first enrolling Windows 365 Business Cloud PCs into [Microsoft Intune](/mem/intune/fundamentals/what-is-intune#key-features-and-benefits).

## Requirements

- You must have the Windows 365 Administrator role.
- An Intune license subscription. For more information, see [Microsoft Intune licensing](/mem/intune/fundamentals/licenses).

## Change setting to allow admins to enroll Cloud PCs in Intune

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Make sure that the [Mobile Device Management Authority in Intune is set to Intune MDM Authority](/mem/intune/fundamentals/mdm-authority-set).
3. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) and select **Update organization settings**.
4. Select **Enroll new Cloud PCs in Microsoft Intune** > **Save**.

After enrolling Cloud PCs in Intune, you can add apps as explained in [Add Microsoft 365 Apps to Windows 10/11 devices with Microsoft Intune](/mem/intune/apps/apps-add-office365).

> [!NOTE]
>
> Enrolling Windows 365 Business Cloud PCs into Intune won't grant access to the **Cloud PC creation** page in Intune. Nor will enrollment grant access to any Windows 365 Enterprise-specific features like connection reports in Endpoint Analytics, custom images, provisioning policies.

## Next steps

[Learn about Microsoft Intune app management](/mem/intune/apps/app-management).
