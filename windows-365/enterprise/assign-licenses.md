---
# required metadata
title: Assign licenses for Windows 365
titleSuffix:
description: Learn how to assign licenses for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/15/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
- essentials-manage
---

# Assign licenses

[Windows 365 licenses](https://www.microsoft.com/windows-365/all-pricing) must be assigned before users can use a Cloud PC.

## Windows 365 Enterprise

Before a user can use a Cloud PC, you must assign a [Windows 365 license](https://www.microsoft.com/windows-365/all-pricing) to that user. You can assign the licenses using any of these methods:

- Microsoft 365 admin center for individual users. For steps on how to use admin center to assign licenses, see [Assign licenses to users](/microsoft-365/admin/manage/assign-licenses-to-users).
- [Microsoft Entra admin center](https://aad.portal.azure.com/) for group license assignments. For more information about group license assignments, see [Assign licenses to users by group membership in Microsoft Entra ID](/azure/active-directory/enterprise-users/licensing-groups-assign).
- To assign direct licenses to a list of individual users, see [Assign licenses for Windows 365](/microsoft-365/enterprise/assign-licenses-to-user-accounts-with-microsoft-365-powershell) or see [Assign license](/graph/api/user-assignlicense) to perform through Graph.

## Windows 365 Frontline

Licenses for Windows 365 Frontline are assigned to your tenant and shared across Cloud PCs provisioned in dedicated mode and shared mode. The licenses are assigned by selecting a  Microsoft Entra group during the [creation of provisioning policies](create-provisioning-policy.md).

## Next steps

[Create Azure network connection](create-azure-network-connection.md).
