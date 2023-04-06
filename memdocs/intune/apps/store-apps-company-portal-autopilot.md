---
# required metadata

title: Add and assign the Windows Company Portal app for Intune managed devices
titleSuffix: Microsoft Intune
description: Add and assign the Windows Company Portal app to Intune managed devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/06/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- Windows
- highpri
---

# Add and assign the Windows Company Portal app for Intune managed devices

To manage devices and install apps, your users can optionally use the Company Portal app. You can assign the Windows Company Portal app directly from Intune using [Microsoft Store app (new)](store-apps-microsoft.md) apps.

## Prerequisites

You can choose to install the **Company Portal** app using the steps below. The Company Portal app will be installed in device context (also known as system-context) when assigned to the Autopilot group and will be installed on the device before the user logs in. 

## Create and Assign the Company Portal app

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with your admin account.
2. Select **Apps** > **All apps** > **Add**.
3. In **Select app type** pane, select **Microsoft Store app (new)** under the **Store app** section.
4. Choose **Select** at the bottom of the page to begin creating an app from the Microsoft Store.
5. Select **Search the Microsoft Store app (new)**.
6. Enter the text **Company Portal**, select **Company Portal**, then choose **Select** at the bottom of the page.
7. Change **Install behaviour** to **System**, then select **Next**.
8. Select scope tags as necessary, then select **Next**.
9. To [Assign](apps-deploy.md) the Company Portal app as a required app to your selected device groups, select > **Add Group** (below **Required**) and then select a device group to assign the app. After you have created all the necessary assignments, select **Next**.
10. Review your settings and select **Create**.

## Next steps

- To learn more about assigning apps, see [Assign apps to groups](apps-deploy.md).
- To learn more about **Microsoft Store app (new)** apps, see [Add Microsoft Store apps to Microsoft Intune](store-apps-microsoft.md).
