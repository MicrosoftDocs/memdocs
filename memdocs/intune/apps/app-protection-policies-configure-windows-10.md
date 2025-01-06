---
# required metadata

title: Configure app protection policies for Windows 10/11
titleSuffix: Microsoft Intune
description: This article describes how to configure app protection policies (APP) for Windows 10/11 devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
- Windows
---

# Get ready for Windows Information Protection in Windows 10/11 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Enable Windows Information Protection (WIP) for Windows 10/11 by setting the WIP provider in Microsoft Entra ID. Setting a WIP provider in Microsoft Entra ID allows you to define the enrollment state when creating a new WIP policy with Intune. The enrollment state can be either WIP or mobile device management (MDM).

>[!IMPORTANT]
> Windows Information Protection (WIP) policies without enrollment has been deprecated. You can no longer create WIP policies for unenrolled devices.

## To configure the WIP provider

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **All services** and choose **M365 Microsoft Entra ID** to switch dashboards.
3. Select **Microsoft Entra ID**.
4. Choose **Mobility (MDM and WIP)** in the **Manage** group.
5. Select **Microsoft Intune**.
6. Configure the settings in the  **Restore default WIP URLs** group on the **Configure** pane.

   **WIP user scope**  
   Use WIP autoenrollment to manage enterprise data on your employees' Windows devices. WIP autoenrollment will be configured for your own device scenarios.<ul><li>**None**<br>Select if no users can be enrolled in WIP.</li><li>**Some**<br>Select Microsoft Entra groups that contain users who will be enrolled in WIP.</li><li>**All**<br>Select if all users can be enrolled in WIP.</li></ul>

   **WIP terms of use URL**  
   The WIP terms of use URL isn't supported for Microsoft Intune. This input box must be left blank for protection policies to apply.

   **WIP discovery URL**  
   The URL of the enrollment endpoint of the WIP service. The enrollment endpoint is used to enroll devices for management with the WIP service.

   **WIP compliance URL**  
   The WIP compliance URL isn't supported for Microsoft Intune. This input box must be left blank for protection policies to apply. 

7. Select **Save**.

## Next steps

[Create a WIP policy.](windows-information-protection-policy-create.md)
