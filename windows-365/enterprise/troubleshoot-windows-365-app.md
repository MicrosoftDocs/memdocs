---
# required metadata
title: Troubleshoot the Windows 365  app.
titleSuffix:
description: Troubleshoot the Windows 365 app.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/12/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkhoff
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Troubleshoot the Windows 365 app (preview)

This article describes issues with the Windows 365 app ([preview](../public-preview.md)) for Windows client and how to fix them.

## Limitations

The Windows 365 app doesn't currently support:

- Windows 10
- Windows 11 IoT
- Configuring Remote Desktop Protocol properties.

## The Windows 365 app doesn’t start the Cloud PC session

When the Remote Desktop Client is installed, you'll see a file type association message after trying to connect to your Cloud PC. Make sure to select **Azure Virtual Desktop (HostApp)** to launch the Cloud PC session.

![Screencap of opening .avd files](./media/troubleshoot-windows-365-app/azure-virtual-desktop.png)

## Change Cloud PC session from full screen to window mode  

The Windows 365 app supports windowed mode to work more efficiently side-by-side with your local PC. To activate window mode, click on the window mode button in the connection bar.  

## Windows 365 app doesn't show any Cloud PCs

You might be signed in as the wrong user. You must be signed in with an account hat is enrolled with the Azure Active Directory (Azure AD) account that has Cloud PCs provisioned. Make sure that you sign in the Windows 365 app with the right user account.

<!-- ########################## -->
## Next steps

[Learn more about Windows 365 App](https://support.microsoft.com/topic/cbb0d4d5-69d4-4f00-b050-6dc7a02d02d0).
