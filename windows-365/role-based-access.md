---
# required metadata
title: Windows 365 role-based access - Azure | Microsoft Docs
titleSuffix:
description: Learn about role-based access control in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/16/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: cohanley
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Role-based access control

Role-based access control (RBAC) helps you manage who has access to your organization's resources and what they can do with those resources. You can assign roles for your Cloud PCs by using the Microsoft Endpoint Manager admin center.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).

## Cloud PC built-in roles

Two new built-in roles are available for Cloud PC:

**Cloud PC Administrator**: Manages all aspects of Cloud PCs, like:

- OS image management
- On-premises network connection configuration
- Provisioning

**Cloud PC Reader**: Views Cloud PC data available in the Cloud PC node in MEM, but can’t make changes.

## Custom roles

Custom roles aren't supported for Cloud PCs.

<!-- ########################## -->
## Next steps
[Role-based access control (RBAC) with Microsoft Intune](/mem/intune/fundamentals/role-based-access-control).
