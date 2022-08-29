---
# required metadata
title: Provide users a localized Windows experience on their Cloud PC
titleSuffix:
description: Learn how to provide a localized Windows experience for your end users.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/11/2022
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Provide a localized Windows experience

For users to be productive on their Windows 365 Cloud PC, it's important for Windows to use a display language that they're comfortable with. Users can always change the display language themselves through the Settings app in Windows. But the Windows experience is more welcoming if the user sees the right language immediately, starting when they first sign in.

There are two different ways to provide a localized Windows experience when users first sign in:

- [Use a provisioning policy](use-provisioning-policy-default-display-language.md). If you plan on using a gallery image, you can select the language when you create the provisioning policy.
- [Create a custom device image](create-custom-image-languages.md). If you plan on using a custom image and you manage your Cloud PCs through group policy, you can include the language as part of the custom image.

## URLs to allow

For both the provisioning policy and custom image options to set up the display languages, make sure to add the following URLs to your firewall allowlist:

- Windows 11 21H2
  - LanguagePack: https://software-download.microsoft.com/download/sg/22000.1.210604-1628.co_release_amd64fre_CLIENT_LOF_PACKAGES_OEM.iso
  - FodToLP: https://download.microsoft.com/download/7/6/0/7600F9DC-C296-4CF8-B92A-2D85BAFBD5D2/Windows-10-1809-FOD-to-LP-Mapping-Table.xlsx
- Windows 10 21H2 and 21H1
  - LanguagePack: https://software-download.microsoft.com/download/pr/19041.1.191206-1406.vb_release_CLIENTLANGPACKDVD_OEM_MULTI.iso
  - FOD: https://software-download.microsoft.com/download/pr/19041.1.191206-1406.vb_release_amd64fre_FOD-PACKAGES_OEM_PT1_amd64fre_MULTI.iso
  - InboxApps: https://software-download.microsoft.com/download/sg/19041.928.210407-2138.vb_release_svc_prod1_amd64fre_InboxApps.iso
- Windows 10 20H2
  - LanguagePack: https://software-download.microsoft.com/download/pr/19041.1.191206-1406.vb_release_CLIENTLANGPACKDVD_OEM_MULTI.iso
  - FOD: https://software-download.microsoft.com/download/pr/19041.1.191206-1406.vb_release_amd64fre_FOD-PACKAGES_OEM_PT1_amd64fre_MULTI.iso
  - InboxApps: https://software-download.microsoft.com/download/pr/19041.508.200905-1327.vb_release_svc_prod1_amd64fre_InboxApps.iso
- Windows 10 1909
  - LanguagePack: https://software-download.microsoft.com/download/pr/18362.1.190318-1202.19h1_release_CLIENTLANGPACKDVD_OEM_MULTI.iso
  - FOD: https://software-download.microsoft.com/download/pr/18362.1.190318-1202.19h1_release_amd64fre_FOD-PACKAGES_OEM_PT1_amd64fre_MULTI.iso
  - InboxApps: https://software-download.microsoft.com/download/pr/18362.1.190318-1202.19h1_release_amd64fre_InboxApps.iso

## Next steps

[Use a provisioning policy](use-provisioning-policy-default-display-language.md) or [create a custom device image](create-custom-image-languages.md) to set up the display language.
