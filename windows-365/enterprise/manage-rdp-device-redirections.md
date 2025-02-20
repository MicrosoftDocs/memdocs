---
# required metadata
title: Manage device RDP redirections for Cloud PCs.
titleSuffix:
description: Learn how to Use the Windows 365 deployment checklist during your deployment.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2024
ms.topic: conceptual
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
---

# Manage RDP device redirections for Cloud PCs

Remote Desktop Protocol (RDP) can be used to create redirections that let users connect to peripherals (like cameras, USB drives, and printers) from remote devices like Cloud PCs. By default, these redirections are enabled for Cloud PCs. Update these redirections according to your organization's policies.

To understand which redirections are supported based on which platform is used to access the Cloud PC, see [Compare the clients: redirections](/windows-server/remote/remote-desktop-services/clients/remote-desktop-app-compare).

## RDP device redirection settings

The following redirections can be managed by using the appropriate setting:

| Redirection | Group policy |
| --- | --- |
| Audio input | Allow audio recording redirection |
| Audio output | Allow audio and video playback redirection |
| Cameras | Do not allow video capture redirection |
| Clipboard | Do not allow Clipboard redirection |
| COM ports | Do not allow COM port redirection |
| Drives | Do not allow drive redirection |
| Location | Do not allow location redirection |
| Printers | Do not allow client printer redirection |
| Smartcards | Do not allow smart card device redirection |
| USB drives| Do not allow supported Plug and Play device redirection |

Some settings may not be immediately available in the Settings Catalog.

There are two ways to manage these redirections:

- Settings Catalog: Use a device configuration policy in Microsoft Intune. Supports both Microsoft Entra join and Microsoft Entra hybrid join Cloud PCs.
- Group Policy Object (GPO): Use GPOs in Windows Server Active Directory. Supports Microsoft Entra hybrid join Cloud PCs only.

Follow the appropriate guidance to manage RDP device redirections.

## Use the Settings Catalog to manage RDP device redirections

To manage any of the redirections by using the Settings Catalog, create and assign a device configuration policy:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile**.

2. Select the **Windows 10 and later** platform, the **Settings catalog** profile type, then **Create**.

3. On the **Basics** page, enter a **Name** and **Description** (optional) for the new policy.

4. On the **Configuration settings** page, select **+ Add settings** to list and select settings to manage.

    - To manage printer redirection settings, search for *Printer Redirection*, select the resulting category, and select the settings you want to manage.
    - To manage other redirection settings, search for “Device and Resource Redirection”, select the resulting category, and select the settings you want to manage.

5. After you select all the redirection settings that you want to manage, close the **Settings picker** view, configure the settings on the **Configuration settings** page, then select **Next**.

6. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

7. On the **Assignments** page, select the users or groups that you want to receive the redirection policy, then select **Next**.

8. On the *Review + create** page, select **Create**.

For more help using the settings catalog to create a device configuration policy, see [Use the settings catalog to configure settings on Windows and macOS devices](/mem/intune-service/configuration/settings-catalog).

> [!Note]
> The settings catalog configures policies by using the Policy CSP. To make sure that these settings take precedence over a conflicting GPO, you can also configure the [ControlPolicyConflict CSP]( /windows/client-management/mdm/policy-csp-controlpolicyconflict#controlpolicyconflict-policies).

## Use a GPO to manage RDP device redirections

To manage any of the redirections by using GPO, create and assign a GPO in your Windows Server Active Directory domain. Make sure to use the corresponding policies as shown in the [RDP device redirection settings table](#rdp-device-redirection-settings). To learn more about the policies, download the [Group Policy Settings Reference Spreadsheet](https://www.microsoft.com/download/101451).

## Clipboard redirections

Clipboard redirection in Azure Virtual Desktop and Windows 365 lets users copy and paste content (like text, images, and files) between the user's device and the remote session in either direction. For more information, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types?tabs=intune).

<!-- ########################## -->
## Next steps

[Learn about apps in Windows 365](app-overview.md).
