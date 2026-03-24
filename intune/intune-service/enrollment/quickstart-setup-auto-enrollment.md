---
title: Set up automatic enrollment in Intune
description: Enable Intune automatic enrollment of Windows devices that join or register with your Microsoft Entra ID.
services: microsoft-intune
ms.topic: how-to
ms.date: 01/27/2026
ms.reviewer: maholdaa
ms.collection:
- M365-identity-device-management
- highpri
---

# Step 4 - Set up automatic enrollment for Windows devices

In this article, you set up Microsoft Intune to automatically enroll Windows corporate-owned devices, and user-owned devices for bring-your-own-device (BYOD) deployments. You can scope automatic enrollment to some Microsoft Entra users, all users, or no users.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> - A Microsoft Intune subscription. [Sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
> - [Microsoft Entra ID P1 or P2](/azure/active-directory/active-directory-get-started-premium) or the [Premium trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845). You can activate a free Premium trial subscription during setup.
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
> - [Create a user](../fundamentals/quickstart-create-user.md).
> - [Create a group](../fundamentals/quickstart-create-group.md).
:::column-end:::
:::row-end:::

## Set up automatic enrollment

In this example, you configure Microsoft Intune mobile device management (MDM) enrollment settings so that corporate-owned and personal devices automatically enroll in Microsoft Intune. *MDM user scope* enables automatic enrollment for Microsoft Intune device management.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
2. Go to the **Windows** tab. Then select **Automatic Enrollment**.

    > [!IMPORTANT]
    > Automatic MDM enrollment is a premium Microsoft Entra feature available for Microsoft Entra ID Premium subscribers. If you can't see the automatic enrollment settings, select **Automatic MDM enrollment is available only for Microsoft Entra ID Premium subscribers** to activate a free trial.

3. Select **Microsoft Intune**.
4. Configure the MDM and WIP user scope.
   1. For **MDM user scope** select **All**. Or you can select **Some** and select **Contoso Testers** as the group. Make sure users aren't members of a group targeted by the WIP user scope.
   1. For **WIP user scope**, select **None**. You're only setting up automatic enrollment for mobile device management.
5. Use the default values for the remaining settings on the page.
6. Choose **Save**.

>[!IMPORTANT]
> If you configure both user scope types for the same user:
>
> - The MDM user scope takes precedence if they're on a corporate-owned device. The device automatically enrolls in Microsoft Intune when they set it up for work.
> - The WIP user scope takes precedence if they bring their own device. The device doesn't enroll in Microsoft Intune for device management. Microsoft Purview Information Protection policies are applied if you configured them.

## Clean up resources

To reconfigure Intune automatic enrollment, see [Set up enrollment for Windows devices](windows-enroll.md).

## Next steps

In this task, you learned how to set up automatic enrollment for devices running Windows. For more information about device enrollment, see [Device enrollment overview](../fundamentals/deployment-guide-enrollment.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 5 - Enroll your Windows device](quickstart-enroll-windows-device.md)
