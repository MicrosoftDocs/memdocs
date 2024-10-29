---
title: Manage your Windows 365 Business Cloud PCs
description: Learn how to manage your Windows 365 Business Cloud PCs
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 08/28/2024
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
- tier2
- essentials-manage
---

# Manage Cloud PCs

You can remotely manage Windows 365 Business Cloud PCs by using the Microsoft 365 admin center or windows365.microsoft.com. Each supports several remote management actions. To use these remote actions, you must have the following Microsoft Entra role-based access role:

   - Windows 365 administrator

As a user with one of the above admin roles assigned, you can manage Cloud PCs in your organization in various ways:

## windows365.microsoft.com

You can sign in to [windows365.microsoft.com](https://windows365.microsoft.com) to:

- [Add a user and assign a license](add-user-assign-licenses.md).
- [Assign or unassign licenses](assign-unassign-license.md).
- [Change organization default settings](change-organization-default-settings.md).
- [Use remote actions on Cloud PCs](remotely-manage-business-cloud-pcs.md).
- [Reset a user's password](reset-user-password.md).

## Microsoft 365 admin center

You can sign in to the [Microsoft 365 admin center](https://admin.microsoft.com) to [use remote actions on Cloud PCs](remotely-manage-business-cloud-pcs.md).

## Intune

If the organization and users are properly licensed, Cloud PCs can be enrolled in Intune. In this case, use the same procedure for [enrolling Windows 10 machines in Intune](/mem/intune/user-help/enroll-windows-10-device).

## Microsoft Graph

You can also use the Microsoft Graph APIs to manage Cloud PCs. For more information, see [Overview for Windows 365 Cloud PC on Microsoft Graph](/graph/cloudpc-concept-overview).

## Next steps

[Troubleshoot](troubleshoot-windows-365-business.md)
