---
# required metadata
title: Change organizational default settings in Windows 365 Business
titleSuffix:
description: Learn how to change organizational default settings in Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/08/2021
ms.topic: how-to
ms.service: cloudpc
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
ms.collection: M365-identity-device-management
---

# Change organizational default settings

By default, new Cloud PCs are created with the Windows 11 operating system and the Standard User account type. You can change these defaults by following these steps:

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) with an Azure Active Directory (Azure AD) Global Administrator account.
2. Select **Your organization’s Cloud PCs** > **Update organization settings**.
3. Select your preferred operating system and account type > **Save**.
    ![Screenshot of default settings](/media/change-organization-default-settings/change-organization-default-settings.png)

Organization settings only apply to newly created Cloud PCs. When these settings are changed, they won’t change the OS or account type of existing Cloud PCs.

> [!NOTE]  
> The 1 vCPU/2 GB RAM/64 GB storage license doesn’t support the Windows 11 minimum hardware requirements. When this license is assigned to a user, they will always receive a Windows 10 Cloud PC.
