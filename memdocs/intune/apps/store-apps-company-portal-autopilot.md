---
# required metadata

title: Add and assign the Windows 10 Company Portal app for Autopilot provisioned devices
titleSuffix: Microsoft Intune
description: Add and assign the Windows 10 Company Portal app to Intune for Autopilot provisioned devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
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

You can choose to install the **Company Portal (Offline)** app using the steps below. The Company Portal app will be installed in device context when assigned to the Autopilot group and will be installed on the device before the user logs in.

## Configure the store settings to show the offline app

1. Sign in to the [Microsoft Store for Business](https://www.microsoft.com/business-store) with your admin account.
2. Select the **Manage** tab near the top of the window.
3. In the left pane, select **Settings**.
4. Under **Shopping experience**, set **Show offline apps** to **On**.  
   The offline licensed apps are displayed.

## Get the offline Company Portal app from the store

1. Search for and then select the **Company Portal** app.
2. Set the **License type** to **Offline**.
3. Select **Get the app** to acquire and add the offline Company Portal app to your inventory.
   In order for the app to be listed in Intune, you must either wait for the sync schedule to complete or do a manual sync from Microsoft Endpoint Manager admin center.

## Manually sync Company Portal app with Intune

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with your admin account.
2. Select **Tenant administration** > **Connectors and tokens** > **Microsoft Store for Business**.
3. Click **Enable**.
4. If you haven't already done so, click the link to sign up for the Microsoft Store for Business and associate your account as detailed previously.
5. From the **Language** drop-down list, choose the language in which apps from the Microsoft Store for Business are displayed in the Azure portal. Regardless of the language in which they are displayed, they are installed in the end user's language when available.
6. Click **Sync** to get the apps you've purchased from the Microsoft Store into Intune.

## Assign the Company Portal app

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with your admin account.
2. Select **Apps** > **Windows**.
3. From the list of Windows apps, select **Company Portal (Offline)**.
4. To [Assign](apps-deploy.md) the Company Portal app as a required app to your selected autopilot device groups, select Properties, Assignments, Edit, Add Group (below Required) and then select a device Group to assign the app to. As this is an Offline app, be sure to change the 'License Type' to Device licensing before continuing to the 'Review + save' button

## Next steps

- To learn more about assigning apps, see [Assign apps to groups](apps-deploy.md).

