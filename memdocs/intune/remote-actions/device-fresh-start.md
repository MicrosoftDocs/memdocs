---
# required metadata

title: Reset Windows 10 devices with Microsoft Intune
description: Use Fresh Start to remove or uninstall apps on Windows 10 PCs by using Microsoft Intune. 
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Use Fresh Start to reset Windows 10 devices with Intune

The **Fresh Start** device action removes any apps that are installed on a PC running Windows 10, version 1709 or later. Fresh Start helps remove pre-installed (OEM) apps that are typically installed with a new PC.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **All devices**.
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
