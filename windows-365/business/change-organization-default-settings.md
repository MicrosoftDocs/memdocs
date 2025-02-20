---
# required metadata
title: Change organizational default settings in Windows 365 Business
titleSuffix:
description: Learn how to change organizational default settings in Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/21/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-business
ms.localizationpriority: high
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

# Change organizational default settings

By default, new Cloud PCs are created with the following settings:

- **Single sign-on**: Off
- **Account type**: Standard User
- **Operating system**: Windows 11
- **Language and region**: English (United States)
- **Enroll new Cloud PCs in Intune**: Off

You can change these defaults by following these steps:

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) with an account that has the Windows 365 Administrator role.
2. Select **Your organization’s Cloud PCs** > **Update organization settings**.
3. Select your preferred option for the following settings:
    - **Single sign-on**: Select this option to enable a single sign-on experience for users when accessing their Cloud PC. Before turning this option on, review the information to [configure single sign-on](configure-single-sign-on.md).
    - **Account type**: Standard User or Local Administrator.
    - **Operating system**: Windows 11 (recommended) or Windows 10.
    - **Language and region**: Sets the display language, time/date formats, and automatically installs any [Features on Demand](/windows-hardware/manufacture/desktop/features-on-demand-language-fod) like text-to-speech and speech recognition. If the user signs in and doesn't see the correct language, [reset](remotely-manage-business-cloud-pcs.md) the Cloud PC.
    - **Enroll new Cloud PCs in Intune**: Select this option to automatically enroll new Cloud PCs in Intune. This option is only visible to admin accounts that have:
        - An Intune license subscription. For more information, see [Microsoft Intune licensing]( /mem/intune/fundamentals/licenses).
        - [Set up Intune](/mem/intune-service/fundamentals/setup-steps) through step 6 (Set the MDM authority).
4. Select **Save**.

When single sign-on is modified, it applies to all new and existing Cloud PCs. For all the other options, the option only applies to new Cloud PCs created after the chosen setting was modified. When these settings are changed, they won’t change the operating system, account type, language/region, or Intune enrollment of existing Cloud PCs.

You can also change your organization's default settings in the Microsoft 365 admin center. For more information, see [Change your organization's address, technical contact, and more](/microsoft-365/admin/manage/change-address-contact-and-more).

## Notes

### Operating system

The 1 vCPU/2 GB RAM/64 GB storage license doesn’t support the Windows 11 minimum hardware requirements. When this license is assigned to a user, they'll always receive a Windows 10 Cloud PC.

### Language and region

To change the language settings on an already-created Cloud PC, see [Language packs for Windows 10](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_10) and [Language packs for Windows 11](https://support.microsoft.com/windows/language-packs-for-windows-a5094319-a92d-18de-5b53-1cfc697cfca8#WindowsVersion=Windows_11).

### Enrolling Cloud PCs in Intune

To enroll devices that have already been created, ask your users to follow this [guide for enrollment in Intune](/mem/intune-service/enrollment/quickstart-enroll-windows-device).

Windows 365 Enterprise-specific features, like custom images and provisioning policies, aren’t available to Windows 365 Business customers, even if Cloud PCs are enrolled in Intune.  

## Next steps

[Troubleshoot Intune enrollment issues](troubleshoot-windows-365-business.md)
