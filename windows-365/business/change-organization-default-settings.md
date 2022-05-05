---
# required metadata
title: Change organizational default settings in Windows 365 Business
titleSuffix:
description: Learn how to change organizational default settings in Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/09/2022
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

By default, new Cloud PCs are created with the following settings:

- **Account type**: Standard User
- **Operating system**: Windows 11
- **Language and region (preview)**: English (United States)

You can change these defaults by following these steps:

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) with an Azure Active Directory (Azure AD) Global Administrator account.
2. Select **Your organization’s Cloud PCs** > **Update organization settings**.
3. Select your preferred option for the following settings:
    - **Account type**: Standard User or Local Administrator.
    - **Operating system**: Windows 11 (recommended) or Windows 10.
    - **Language and region ([preview](../public-preview.md))**: Sets the display language, time/date formats, and automatically installs any [Features on Demand](/windows-hardware/manufacture/desktop/features-on-demand-language-fod) like text-to-speech and speech recognition. This setting only localizes the Windows experience. For changing the language in MIcrosoft 365 apps, see [Language Accessory Pack for Office](https://support.microsoft.com/office/language-accessory-pack-for-office-82ee1236-0f9a-45ee-9c72-05b026ee809f). If the user signs in and doesn't see the correct language, [reset](remotely-manage-business-cloud-pcs.md) the Cloud PC (this deletes all data on the Cloud PC and reinstall the language pack).
4. Select **Save**.

All new Cloud PCs will be created with the chosen settings. When these settings are changed, they won’t change the operating system, account type, or language/region of existing Cloud PCs.

You can also change your organization's default settings in the Microsoft 365 admin center. For more information, see [Change your organization's address, technical contact, and more](/microsoft-365/admin/manage/change-address-contact-and-more).

To change the language settings on an already-created Cloud PC, see [Language packs for Windows 10](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_10) and [WLanguage packs for indows 11](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_11).

> [!NOTE]  
> The 1 vCPU/2 GB RAM/64 GB storage license doesn’t support the Windows 11 minimum hardware requirements. When this license is assigned to a user, they will always receive a Windows 10 Cloud PC.
