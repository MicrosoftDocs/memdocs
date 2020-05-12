---
# required metadata

title: Reset Windows 10 devices with Microsoft Intune - Azure | Microsoft Docs
description: Use Fresh Start to remove or uninstall apps on Windows 10 PCs by using Microsoft Intune. 
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use Fresh Start to reset Windows 10 devices with Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Fresh Start** device action removes any apps that are installed on a PC running Windows 10, version 1709 or later. Fresh Start helps remove pre-installed (OEM) apps that are typically installed with a new PC. 

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **All devices**.
2. From the list of devices you manage, choose a Windows 10 desktop device.
3. Click **Fresh Start**. 
4. Select **Retain user data on this device** to:
   * Keep the device Azure AD joined
   * Device is enrolled into mobile device management again when an Azure Active Directory enabled user signs into the device.
   * Keep the contents of the device user's Home folder, and remove apps and settings

  > [!IMPORTANT]
 > If you do not retain user data, the device will be restored to the default OOBE (out-of-box experience) completed state retaining the built in administrator account.
 > BYOD devices will be unenrolled from Azure AD and mobile device management.
 > Azure AD joined devices will be enrolled into mobile device management again when an Azure Active Directory enabled user signs into the device.
 
5. Click **OK**.   
6. To see the status of this action, go back to **Devices** and click **Device actions**.  
7. The device will be restored to the initial sign-in screen.
