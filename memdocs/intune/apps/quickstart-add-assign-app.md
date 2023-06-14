---
# required metadata

title: Add and assign an app
titleSuffix: Microsoft Intune
description: In this topic, you will use Microsoft Intune to add and assign an app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/19/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: dab6f5c8-1ebb-42c4-a7a7-7af001f94e15

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Step 8: Add and assign an app

In this topic, you will use Intune to add and assign an app to your company's workforce. One of an admin's priorities is to ensure that end users have access to the apps they need to do their work.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

- To complete this evaluation step, you must [create a user](../fundamentals/quickstart-create-user.md), [create a group](../fundamentals/quickstart-create-group.md), and [enroll a device](../enrollment/quickstart-setup-auto-enrollment.md).

## Sign in to Intune

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a [Global administrator or an Intune Service administrator](../fundamentals/users-add.md#types-of-administrators). If you have created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Add the app to Intune

An app can be included so that Intune can manage aspects of the app. 

Use the following steps to add an app to Intune:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. 
2. In the **App type** drop-down box, select **Windows 10 and later** from **Microsoft 365 Apps**.
3. Click **Select**. The **Add app** steps are displayed.
4. Confirm the default details in the **App suite information** step and click **Next**.
5. Confirm the default settings in the **App settings** step and click **Next**.
6. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
7. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
13. When you are done, click **Create** to add the app to Intune.

## Assign the app to a group

After you've added an app to Microsoft Intune, you can assign the app to additional groups of users or devices.

> [!NOTE]
> This evaluation step builds on previous evaluation steps in this series. Please see [prerequisites](quickstart-add-assign-app.md#prerequisites) in this topic for details.

Use the following steps to assign an app to a group:

1. In [Intune](https://aka.ms/intuneportal), select **Apps** > **All apps**. 
2. Select the app that you want to assign to a group.
3. Click **Properties**. Next to **Assignments** click **Edit**. 
5. Click **Add Group** under the **Required** section. The **Select group** pane is displayed.
6. Find the group that you need to added and click **Select** at the bottom of the pane. 
1. Click **Review + save** > **Save** to assign the group.

You now have assigned the app to an additional group.

## Install the app on the enrolled device

End users must install and use the Company Portal app to install an app made available by Intune. You, acting as an end user, can use the following steps to verify that the app is available to the user of the enrolled device.

1. Log in to your enrolled Windows 10 Desktop device.

    > [!IMPORTANT]
    > The device must be [enrolled with Intune](../enrollment/quickstart-enroll-windows-device.md). Also, you must sign in to the device using an account contained in the group you assigned to the app.

2. From the **Start** menu, open the **Microsoft Store**. Then, find the **Company Portal** app and install it.
3. Launch the **Company Portal** app.
4. Click the app that you added using Intune. In this topic you added the **Microsoft 365 Apps** suite.

    > [!NOTE]
    > If you did not successfully assign any apps to the Intune user, you will see the following message:
    > *Your IT administrator did not make any apps available to you.*

5. Click **Install**.

If your business needs require that you assign the Company Portal app to your workforce, you can manually assign the Windows 10 Company Portal app directly from Intune. For more information see, [Manually add the Windows 10 Company Portal app by using Microsoft Intune](company-portal-app.md).

## Next steps

In this topic, you added apps to Intune, assigned the apps to a group, and installed the apps on the enrolled Windows 10 Desktop device. For more information about managing apps in Intune, see [What is Microsoft Intune app management?](app-management.md)

To continue to evaluate Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 9: Create and assign an app protection policy](quickstart-create-assign-app-policy.md)
