---
title: Create a Password Compliance Policy for Android Enterprise
description: Create a password compliance policy in Microsoft Intune for Android Enterprise devices. Learn to require specific password lengths to meet your organization's security requirements.
author: nicholasswhite
ms.author: nwhite
ms.date: 01/15/2026
ms.topic: article
ms.reviewer: andreibiswas
ms.collection:
- M365-identity-device-management
- Android
- sub-device-compliance
---

# Step 6 - Create a password compliance policy for Android Enterprise devices

In this article, you use Microsoft Intune to create a password compliance policy for Android Enterprise devices. This policy requires your Android users to enter a password of a specific length to be compliant with your organization's security requirements. You can create a password compliance policy for any device platform that Intune supports. This example uses Android Enterprise.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

An Intune device compliance policy specifies the rules and settings that devices must meet to be considered compliant. You can enforce these compliance policies by using Microsoft Entra Conditional Access, which you can use to allow or block access to company resources. You can also get device reports and take actions for non-compliance.

> [!IMPORTANT]
> In addition to password settings, consider other system security settings to protect your workforce. For more information, see [System security settings](compliance-policy-create-android-for-work.md).

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
> - Built-in **[Policy and Profile manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager)** Microsoft Intune role
:::column-end:::
:::row-end:::

## Create a device compliance policy

Create a device compliance policy that requires your Android users to enter a password of a specific length.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **Compliance**.
1. On the **Policies** tab, select **Create policy**.
1. For **Platform**, select **Android Enterprise**.

1. For **Profile type**, select either **Fully managed, dedicated, and corporate-owned work profile** or **Personally-owned work profile**, and then select **Create**.

1. On **Basics**, enter **Android compliance** as the *Name*. Adding a *Description* is optional. Select **Next**.

1. On **Compliance settings**, expand **System Security** and configure the following settings:

   - For **Require a password to unlock mobile devices**, select **Require**.
   - For **Required password type**, select **At least numeric**.
   - For **Minimum password length**, enter **6**.

    :::image type="content" source="./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png" alt-text="Screenshot of Microsoft Intune admin center showing Compliance settings for Android with password requirements highlighted." lightbox="./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png":::

1. On the **Assignments**, you can optionally assign the policy to the user or group you created in [Step 2 - Create a user and assign a license](../fundamentals/quickstart-create-user.md) and [Step 3 - Create a group](../fundamentals/quickstart-create-group.md) evaluation steps.

1. When done, select **Next** until you reach the **Review + create** step. Then, select **Create** to create the policy.

When you successfully create the policy, it appears in your list of device compliance policies.

## Conditional Access policy assignment

With the free trial, you can create a Conditional Access policy that enforces this password requirement. This tutorial doesn't include these steps but you can do it.

For more information, see:

- [Learn about Conditional Access and Intune](conditional-access.md)
- [Common ways to use Conditional Access with Intune](../protect/conditional-access-intune-common-ways-use.md)

## Clean up resources

When you no longer need the policy, delete it. To delete the policy, select the compliance policy and select **Delete**.

## Next steps

In this article, you used Intune to create a compliance policy for your Android Enterprise devices that requires a password with at least six characters. For more information about creating compliance policies, see [Get started with device compliance policies in Intune](device-compliance-get-started.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 7 - Send notifications to noncompliant devices](quickstart-send-notification.md)
