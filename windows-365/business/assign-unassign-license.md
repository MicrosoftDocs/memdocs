---
# required metadata
title: Assign or unassign a license in Windows 365 Business
titleSuffix:
description: Learn how to assign or unassign a license in Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/28/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- M365-identity-device-management
- tier2
---

# Assign or unassign a license

You can assign some licenses on [windows365.microsoft.com](https://windows365.microsoft.com).  For full license management, use the [Microsoft 365 admin center](https://admin.microsoft.com).

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) with an Azure Active Directory (Azure AD) Global Administrator account.
2. Select **Your organization’s Cloud PCs**.
3. Select the user whose licenses you want to manage.
4. Select **Licenses and apps**.
5. Select licenses that you want to assign to the user, or deselect licenses that you want to unassign from the user.
6. Select **Save changes**.
    - When you assign a Windows 365 license, Windows 365 will immediately begin creating a new Cloud PC for the user.
    - When you unassign a Windows 365 license from a user or the license expires, that user can still access their Cloud PC for 24 hours. After that time, the Cloud PC will be deleted.
