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
- **Enroll new Cloud PCs in Microsoft Endpoint Manager**: Off

You can change these defaults by following these steps:

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) with an Azure Active Directory (Azure AD) Global Administrator account.
2. Select **Your organization’s Cloud PCs** > **Update organization settings**.
3. Select your preferred option for the following settings:
    - **Account type**: Standard User or Local Administrator.
    - **Operating system**: Windows 11 (recommended) or Windows 10.
    - **Language and region ([preview](../public-preview.md))**: Sets the display language, time/date formats, and automatically installs any [Features on Demand](/windows-hardware/manufacture/desktop/features-on-demand-language-fod) like text-to-speech and speech recognition. If the user signs in and doesn't see the correct language, [reset](remotely-manage-business-cloud-pcs.md) the Cloud PC.
    - **Enroll new Cloud PCs in Microsoft Endpoint Manager**: Select this option to automatically enroll new Cloud PCs in Intune. To see this option, you must have an admin account with an Intune license subscription. For more information, see [Microsoft Intune licensing]( /mem/intune/fundamentals/licenses).
4. Select **Save**.

All new Cloud PCs will be created with the chosen settings. When these settings are changed, they won’t change the operating system, account type, language/region, or Intune enrollment of  of existing Cloud PCs.

You can also change your organization's default settings in the Microsoft 365 admin center. For more information, see [Change your organization's address, technical contact, and more](/microsoft-365/admin/manage/change-address-contact-and-more).

## Notes

### Operating system

The 1 vCPU/2 GB RAM/64 GB storage license doesn’t support the Windows 11 minimum hardware requirements. When this license is assigned to a user, they will always receive a Windows 10 Cloud PC.

### Language and region

To change the language settings on an already-created Cloud PC, see [Language packs for Windows 10](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_10) and [Language packs for Windows 11](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_11).

### Automatically enroll in Intune

To enroll devices that have already been created, ask your users to follow this [guide for enrollment in Intune](/mem/intune/enrollment/quickstart-enroll-windows-device).

Windows 365 Enterprise-specific features, like custom images and provisioning policies, aren’t available to Windows 365 Business customers, even if Cloud PCs are enrolled in Intune.  
