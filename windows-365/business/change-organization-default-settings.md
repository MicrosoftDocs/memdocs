---
# required metadata
title: Change organizational default settings in Windows 365 Business
titleSuffix:
description: Learn how to change organizational default settings in Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/08/2022
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

You can also change your organization's default settings in the Microsoft 365 admin center. For more information, see [Change your organization's address, technical contact, and more](/microsoft-365/admin/manage/change-address-contact-and-more).

Organization settings only apply to newly created Cloud PCs. When these settings are changed, they won’t change the OS or account type of existing Cloud PCs.

> [!NOTE]  
> The 1 vCPU/2 GB RAM/64 GB storage license doesn’t support the Windows 11 minimum hardware requirements. When this license is assigned to a user, they will always receive a Windows 10 Cloud PC.
