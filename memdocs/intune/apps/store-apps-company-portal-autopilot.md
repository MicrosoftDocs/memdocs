---
# required metadata

title: Add and assign the Windows 10 Company Portal app for Autopilot provisioned devices
titleSuffix: Microsoft Intune
description: Add and assign the Windows 10 Company Portal app to Intune for Autopilot provisioned devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add and assign the Windows 10 Company Portal app for Autopilot provisioned devices

To manage devices and install apps, your users can use the Company Portal app. You can assign the Windows 10 Company Portal app directly from Intune. 

## Prerequisites

For Windows 10 Autopilot provisioned devices, it is recommended that you associate your Microsoft Store for Business account with Intune. For more information, see [How to manage volume purchased apps from the Microsoft Store for Business with Microsoft Intune](windows-store-for-business.md).

Company Portal (Offline) is chosen to be installed by using the steps below. The Company Portal app will be installed in device context when assigned to the Autopilot group and be installed on the device before the user logs in. 

## Configure settings to show offline app

1. Sign in to the [Microsoft Store for Business](https://www.microsoft.com/business-store) with your admin account.
2. Select the **Manage** tab near the top of the window.
3. In the left pane, select **Settings**.
4. Under **Shopping experience**, set **Show offline apps** to **On**.  
    The offline licensed apps are displayed.

## Get the offline Company Portal app

1. Search for and then select the **Company Portal** app.
2. Set the **License type** to **Offline**.
3. Select **Get the app** to acquire and add the offline Company Portal app to your inventory.

## Assign the Company Portal app

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with your admin account. 
2. Select the **Apps** tab on the right pane.
3. Under **By platform**, select **Windows**.
4. Select **Company Portal (Offline)**.
5. You must either Wait for the sync schedule to complete or do a manual sync from Microsoft Endpoint Manager admin center.
6. Assign the Company Portal app as a required app to your selected autopilot device groups.

## Next steps

- To learn more about assigning apps, see [Assign apps to groups](apps-deploy.md).

