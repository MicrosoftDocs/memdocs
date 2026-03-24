---
title: Enroll a Windows device
description: Learn how to enroll a Windows device into Microsoft Intune. Follow this step-by-step evaluation guide to test device enrollment and verify it in the Intune admin center.
services: microsoft-intune
ms.date: 01/20/2026
ms.topic: how-to
ms.reviewer: maholdaa
ms.collection:
- M365-identity-device-management
- highpri
---

# Step 5 - Enroll a Windows device in Microsoft Intune

Enrollment ensures that all devices trying to access data within your organization are secure and compliant with your policies and requirements. Upon enrollment, the device gets access to resources like work email, files, VPN, and Wi-Fi. Employees and students who want remote access to work or school resources can also enroll their devices into Microsoft Intune.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

In this article, you:

* Try out the device user experience by enrolling a device running Windows into Microsoft Intune.
* Try out the admin user experience by verifying the enrollment in the Microsoft Intune admin center.

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
> - Built-in **[Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)** Microsoft Entra role
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To complete this step, you must:
> - Complete the evaluation step for [setting up automatic enrollment in Intune](quickstart-setup-auto-enrollment.md).
> - Be using a [supported Windows version](../fundamentals/supported-devices-browsers.md).
:::column-end:::
:::row-end:::

## Enroll device

These steps guide you through using the Settings app on a Windows device to enroll the device into Intune.

1. On the device, open the Settings app, and select **Accounts**.

2. Select **Access work or school**.

3. Select **Connect** to add a work or school account.

    :::image type="content" source="./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png" alt-text="Screenshot of Windows Settings, Accounts section, showing Access work or school with Connect button highlighted." lightbox="./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png":::

4. Enter the username and password for your work account. If you followed the [create a user and assign a license](../fundamentals/quickstart-create-user.md) evaluation step, you can use the user account that you created.

5. Wait for your device to finish registering. When you see the **You're all set!** screen, select **Done**. Your work account should now be visible under **Accounts**.

   :::image type="content" source="./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png" alt-text="Screenshot of Windows Settings showing a connected work or school account under Access work or school." lightbox="./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png":::

    If you followed the previous steps, but still can't access your work or school email account and files, see [Troubleshoot Windows device access](../user-help/troubleshoot-your-windows-10-device-windows.md).

When the device is enrolled in Intune, it starts to receive the Intune policies you create. [Common questions, answers, and scenarios with policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md) provides more information about how policies and profiles work in Intune.

## Confirm device enrollment

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices** to view the enrolled devices in Intune.
3. Verify that you have an additional device enrolled within Intune.

## Clean up resources

To unenroll the device, see [Remove your Windows device from management](../user-help/unenroll-your-device-from-intune-windows.md).

## Next steps

In this task, you learned how to enroll a Windows device into Intune. For more information about the user experience on the device, see the following resources:

- [Windows device enrollment with Intune Company Portal](../user-help/device-enrollment-overview-windows.md)
- [What info can your company see when you enroll your device?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)

You can also automate Windows device enrollment. To learn more, see [Windows enrollment guide for Microsoft Intune](../fundamentals/deployment-guide-enrollment-windows.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 6 - Set a required password length for Android devices](../protect/quickstart-set-password-length-android.md)
