---
title: Create and Assign an App Protection Policy
description: In this article, you use Microsoft Intune to create and assign and app protection policy.
ms.topic: how-to
ms.date: 02/28/2025
ms.reviewer: dagerrit
ms.collection:
- M365-identity-device-management
- FocusArea_Apps_Protect
---

# Step 9: Create and Assign an App Protection Policy

In this article, you use Intune to create and assign an app protection policy to a client app on an end user's device. Intune uses app protection policies to confirm that your apps are meeting your organization's data protection requirements.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

- To complete this evaluation step, you must [create a user](../fundamentals/quickstart-create-user.md), [create a group](../fundamentals/quickstart-create-group.md), [enroll a device](../enrollment/quickstart-setup-auto-enrollment.md), and [add and assign an app](quickstart-add-assign-app.md).

## Sign in to Intune

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as the built-in **[Application Manager](../fundamentals/role-based-access-control-reference.md#application-manager)** Intune role.

If you created an Intune Trial subscription, the account that created the subscription is a Microsoft Entra [Global Administrator](/entra/identity/role-based-access-control/permissions-reference#global-administrator).

> [!CAUTION]
> [!INCLUDE [global-admin](../includes/global-admin.md)]

## Create an app protection policy

Use the following steps to create an app protection policy:

1. In [Intune](https://aka.ms/intuneportal), select **Apps** > **Protection** > **Create** > **Windows 10**.
2. Enter the following details:

    - **Name**: *Windows 10 content protection*
    - **Description**: *Users associated with this policy won't be able to cut, copy, or paste any content between the assigned app and other nonmanaged apps on the device.*
    - **Enrollment state**: *With enrollment*

3. Under **Protected apps**, select **Add**. The **Add apps** pane is displayed.
4. Choose the apps that must adhere to this policy and select **OK**.
5. Select **Next** to display the **Required settings**.
6. Select **Allow Overrides** to set the Windows Information Protection mode. Selecting this option blocks enterprise data from leaving the protected app.
7. Select **Next** to display the **Advanced settings**.
8. Select **Next** to display the **Assignments**.
9. Select **Select groups to include**, select the group, and select **Select**.
10. Select **Next** to display the **Review + create** step.
11. Select **Create** to create your policy.

You see the app protection policy in Intune.

> [!NOTE]
> App protection policies can only be applied to groups that contain users, not groups that contain devices.

## Next steps

In this article, you created and assigned an app protection policy. Users of the app that have this policy assigned won't be able to cut, copy, or paste any content between the assigned app and other nonmanaged apps on the device. This type of protection helps protect your organization's data. For more information about app protection policies in Intune, see [What are app protection policies?](app-protection-policy.md)

To continue to evaluate Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 10: Create and assign a custom role](../fundamentals/quickstart-create-custom-role.md)
