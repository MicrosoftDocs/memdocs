---
title: Add and Assign an App
description: Learn how to add and assign apps to user groups in Microsoft Intune. Ensure your workforce has access to the apps they need.
ms.date: 01/20/2026
ms.topic: how-to
ms.reviewer: bryanke
ms.collection:
- M365-identity-device-management
- FocusArea_Apps_Add
---

# Step 8 - Add and assign an app in Microsoft Intune

In this article, you use Intune to add and assign an app to your company's workforce. The goal is to assign apps that users need to do their work. For example, you can assign Microsoft 365 Apps so users can read email, and create and edit documents and spreadsheets.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> - A Microsoft Intune subscription. [Sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with the following role:
> - Built-in **[Application Manager](../fundamentals/role-based-access-control-reference.md#application-manager)** Microsoft Intune role
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To complete this step, you must:
> - [Create a user](../fundamentals/quickstart-create-user.md).
> - [Create a group](../fundamentals/quickstart-create-group.md).
> - [Enroll a device](../enrollment/quickstart-setup-auto-enrollment.md)
:::column-end:::
:::row-end:::

## Add the app to Intune

When you add an app to Intune, you assign that app to the users and groups that need it. You can choose to assign the app to any group you choose, including the group you created in [Step 3 - Create a group](../fundamentals/quickstart-create-group.md).

Use the following steps to add an app to Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **All Apps** > **Create**.
2. In the **App type** drop-down box, select **Windows 10 and later** from **Microsoft 365 Apps**.
3. Click **Select**. The **Add app** steps are displayed.
4. Confirm the default details in the **App suite information** step and select **Next**.
5. Confirm the default settings in the **App settings** step and select **Next**.
6. Select the group assignments for the app. You can select the group you created in [Step 3 - Create a group](../fundamentals/quickstart-create-group.md). For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
7. Select **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
8. When you're done, select **Create** to add the app to Intune.

## Update the app assignment (optional)

After you add an app to Microsoft Intune, you can assign the app to more groups of users or devices at any time.

Use the following steps to update an app assignment:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **All Apps**.
2. Select the app that you want to assign to a group.
3. Select **Properties**. Next to **Assignments**, select **Edit**.
4. Select **Add Group** under the **Required** section. The **Select group** pane is displayed.
5. Find the group that you want to add and choose **Select** at the bottom of the pane.
6. Select **Review + save** > **Save** to assign the group.

You now have assigned the app to another group.

## Install the app on the enrolled device

End users must install and use the Company Portal app to install an app made available by Intune. You, acting as an end user, can use the following steps to verify that the app is available to the user on Intune-enrolled devices.

1. Sign in to your enrolled Windows device. You can use the device you enrolled in [Step 5 - Enroll a Windows device in Microsoft Intune](../enrollment/quickstart-enroll-windows-device.md).

    > [!IMPORTANT]
    > - The device must be enrolled in Intune.
    > - You must sign in to the device with an account that belongs to the same group you assigned the app to.

2. From the **Start** menu, open the **Microsoft Store**. Then, find the **Company Portal** app and install it.
3. Launch the **Company Portal** app.
4. Select the app that you added to Intune. In this article, you added the **Microsoft 365 Apps** suite.

    > [!NOTE]
    > If you don't successfully assign any apps to the Intune user, you see the following message:
    > `Your IT administrator did not make any apps available to you.`

5. Select **Install**.

If your business needs require that you assign the Company Portal app to your workforce, you can manually assign the Windows Company Portal app directly from Intune. For more information, see [Manually add the Windows Company Portal app by using Microsoft Intune](company-portal-app.md).

## Next steps

In this article, you added apps to Intune, assigned the apps to a group, and installed the apps on the enrolled Windows device. For more information about managing apps in Intune, see [What is Microsoft Intune app management?](app-management.md)

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 9 - Create and assign an app protection policy](quickstart-create-assign-app-policy.md)
