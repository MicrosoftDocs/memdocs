---
# required metadata
title: Optimize Cisco Webex on a Windows 365 Cloud PC
titleSuffix:
description: Learn how to optimize Cisco Webex on a Windows Cloud PC.
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

ms.reviewer: chbrink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Optimize Cisco Webex on a Windows 365 Cloud PC

Cisco Webex is a 3rd-party application that provides online meeting services including support for virtualized environments like Windows 365 Cloud PCs. The instructions in this article help you optimize traffic for Cisco Webex meetings when using the Microsoft Remote Desktop client on a Windows PC to access a Cloud PC.

To optimize Cisco Webex, you’ll need to:

- Install the Cisco Webex VDI Client on the Cloud PC.
- Install the Webex App VDI plugin on the local Windows PC that the user will use to access the Cloud PC.

> [!NOTE]  
> If you run into issues with Cisco Webex for VDI on your Cloud PC, contact [Cisco support](https://help.webex.com/contact).

## Requirements

These instructions don't support connections through a web browser.

- **Windows 365 app for Windows**
- **Windows Remote Desktop Client**
- **Operating system**: Windows

## Install the Cisco Webex HVD client on the Cloud PC

1. Have the user sign in to the Cloud PC as a local administrator and, in their browser, navigate to the [Webex VDI download page](https://www.webex.com/downloads/teams-vdi.html).
2. In **Release date** column of the table, find the most recent date (for example, 12/14/2021).
3. In the **HVD Installer** column of that row, select the appropriate link for your Windows system (32-bit or 64-bit) to download the MSI.
4. You must set some required switches to install the VDI components. So, to run the MSI, open an elevated command prompt and run the following install command. Replace the path and MSI filename with the correct path and filename that you downloaded.
    `msiexec /i %path%\Webex.msi ALLUSERS=1 ENABLEVDI=1 AUTOUPGRADEENABLED=0`
5. To complete the MSI installer, follow the installation instructions.

Alternatively, the admin can deploy the Cisco Webex VDI client. For more information about deploying apps, see the [Win32 App management guide](/mem/intune/apps/apps-win32-app-management).

## Install the plugin on the local Windows PC

1. Sign in to the Windows PC that will be used to access the Cloud PC.
2. In a browser, navigate to the [Webex VDI download page](https://www.webex.com/downloads/teams-vdi.html).
3. In the table, find the row for the same release as you installed on the Cloud PC. In the **Thin-client Plugin** column of that row, select **Windows 32-bit** or **Windows 64-bit** as appropriate.
4. Run the MSI and follow the installation instructions.

For more information on these installation steps, see [Cisco's Deployment guide for Webex App for Virtual Desktop Infrastructure](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cloudCollaboration/wbxt/vdi/wbx-vdi-deployment-guide/wbx-teams-vdi-deployment_chapter_010.html).

## To use the optimized Cisco Webex client

To benefit from these optimizations, users must sign in to their Cloud PC from a Windows PC. After doing so, the user can open Cisco Webex from the Cloud PC and use the WebEx client optimized for Windows 365 Cloud PC.

## To confirm that the Cisco Webex client is using the optimizations

1. Sign in to the Cloud PC from the Windows client.
2. Open the Cisco Webex client and sign in using your Cisco Webex credentials.
3. Select your user profile icon > **Help** > **Health Checker**.
4. The VDI section of the **Health Checker** shows the status of the optimizations.

## Next steps

For more information about deploying apps, see the [Win32 App management guide](/mem/intune/apps/apps-win32-app-management).
