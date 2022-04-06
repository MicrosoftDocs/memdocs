---
# required metadata

title: Configure app protection policies for Windows 10/11 
titleSuffix: Microsoft Intune
description: This topic describes how to configure app protection policies (APP) for Windows 10/11 devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- M365-identity-device-management
- Windows
---

# Get ready for Windows Information Protection in Windows 10/11 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Enable mobile application management (MAM) for Windows 10/11 by setting the MAM provider in Azure AD. Setting a MAM provider in Azure AD allows you to define the enrollment state when creating a new Windows Information Protection (WIP) policy with Intune. The enrollment state can be either MAM or mobile device management (MDM).

## To configure the MAM provider

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **All services** and choose **M365 Azure Active Directory** to switch dashboards.
3. Select **Azure Active Directory**.
4. Choose **Mobility (MDM and MAM)** in the **Manage** group.
5. Click **Microsoft Intune**.
6. Configure the settings in the  **Restore default MAM URLs** group on the **Configure** pane.

   **MAM user scope**  
   Use MAM auto-enrollment to manage enterprise data on your employees' Windows devices. MAM auto-enrollment will be configured for bring your own device scenarios.<ul><li>**None**<br>Select if no users can be enrolled in MAM.</li><li>**Some**<br>Select Azure AD groups that contain users who will be enrolled in MAM.</li><li>**All**<br>Select if all users can be enrolled in MAM.</li></ul>

   **MAM terms of use URL**  
   The MAM terms of use URL is not supported for Microsoft Intune. This input box must be left blank for protection policies to apply.

   **MAM discovery URL**  
   The URL of the enrollment endpoint of the MAM service. The enrollment endpoint is used to enroll devices for management with the MAM service.

   **MAM compliance URL**  
   The MAM compliance URL is not supported for Microsoft Intune. This input box must be left blank for protection policies to apply. 

7. Click **Save**.

## Next steps

[Create a WIP policy](windows-information-protection-policy-create.md)
