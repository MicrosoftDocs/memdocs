---
# required metadata

title: Quickstart - Add and assign a client app
titleSuffix: Microsoft Intune
description: In this quickstart you will use Microsoft Intune to add and assign a client app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: dab6f5c8-1ebb-42c4-a7a7-7af001f94e15

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Quickstart: Add and assign a client app

In this quickstart, you will use Intune to add and assign a client app to your company's workforce. One of an admin's priorities is to ensure that end users have access to the apps they need to do their work.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

- To complete this quickstart, you must [create a user](../fundamentals/quickstart-create-user.md), [create a group](../fundamentals/quickstart-create-group.md), and [enroll a device](../enrollment/quickstart-setup-auto-enrollment.md).

## Sign in to Intune

Sign in to [Intune](https://aka.ms/intuneportal) as a [Global administrator or an Intune Service administrator](../fundamentals/users-add.md#types-of-administrators). If you have created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Add the client app to Intune

An app can be included so that Intune can manage aspects of the app. 

Use the following steps to add an app to Intune:

1. In [Intune](https://aka.ms/intuneportal), select **Apps** > **All apps** > **Add**. 
2. Select **Windows 10** in the **Microsoft 365 Apps** section of the **Select app type** pane.
3. Click **Select**. The **Add app** steps are displayed.
4. Confirm the default details in the **App suite information** page.
5. Click **Next** to display the **Configure app suite** page.
6. Next to **Update Channel** select **Monthly** from the dropdown box.
7. Confirm the remaining default details in the ***Configure app suite** page.
8. Click **Next** to display the **Scope tags** page.
9. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
10. Click **Next** to display the **Assignments** page.
11. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
12. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
13. When you are done, click **Create** to add the app to Intune.

## Assign the app to a group

After you've added an app to Microsoft Intune, you can assign the app to groups of users or devices.

> [!NOTE]
> This quickstart builds on previous quickstarts in this series. Please see [prerequisites](quickstart-add-assign-app.md#prerequisites) in this quickstart for details.

Use the following steps to assign an app to a group:

1. In [Intune](https://aka.ms/intuneportal), select **Apps** > **All apps**. 
2. Select the app that you want to assign to a group.
3. Click **Assignments** > **Add group** to display the **Add group** pane.
4. Select **Available for enrolled devices** in the **Assignment type** dropdown box. 
5. Click **Included Groups** > **Select groups to include** > **Contoso Testers**.
6. Click **Select** > **OK** > **OK** > **Save** to assign the group.

You now have assigned the app to the **Contoso Testers** group.

## Install the app on the enrolled device

You must install and use the Company Portal app to install the **Contoso's To-Do** app made available by Intune. Use the following steps to verify that the app is available to the user of the enrolled device.

1. Log in to your enrolled Windows 10 Desktop device.

    > [!IMPORTANT]
    > The device must be [enrolled with Intune](../enrollment/quickstart-enroll-windows-device.md). Also, you must sign in to the device using an account contained in the group you assigned to the app.

2. From the **Start** menu, open the **Microsoft Store**. Then, find the **Company Portal** app and install it.
3. Launch the **Company Portal** app.
4. Click the app that you added using Intune. In this quickstart you added the **Microsoft 365 Apps** suite.

    > [!NOTE]
    > If you did not successfully assign any apps to the Intune user, you will see the following message:
    > *Your IT administrator did not make any apps available to you.*

5. Click **Install**.

If your business needs require that you assign the Company Portal app to your workforce, you can manually assign the Windows 10 Company Portal app directly from Intune. For more information see, [Manually add the Windows 10 Company Portal app by using Microsoft Intune](company-portal-app.md).

## Next steps

In this quickstart, you added apps to Intune, assigned the apps to a group, and installed the apps on the enrolled Windows 10 Desktop device. For more information about managing apps in Intune, see [What is Microsoft Intune app management?](app-management.md)

To follow this series of Intune quickstarts, continue to the next quickstart.

> [!div class="nextstepaction"]
> [Quickstart: Create and assign an app protection policy](quickstart-create-assign-app-policy.md)
