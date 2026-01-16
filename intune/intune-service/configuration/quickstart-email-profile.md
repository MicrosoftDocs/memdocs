---
title: Create an Email Device Profile for iOS/iPadOS Devices
description: Learn how to create an email device profile in Microsoft Intune for iOS/iPadOS devices. Configure email settings to help users securely access organization email.
author: MandiOhlinger
ms.author: mandia
ms.date: 01/15/2026
ms.topic: how-to
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
---

# Step 11 - Create an email device profile for iOS/iPadOS in Microsoft Intune

This article is part of a series that walks you through common Intune tasks. In this article, you create an email profile for iOS/iPadOS devices.

The profile includes the required settings that allow a device to connect to your organization's email. Email device profiles help standardize settings across your devices. By using these profiles, end users can access organization email on their personal devices without any confusing setup.

To help safeguard your email, use an email profile to determine if devices are compliant. Then, set up Conditional Access to allow only compliant devices access to email. For details about email profiles, see [How to configure email settings in Microsoft Intune](email-settings-configure.md).

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
> - Built-in **[Policy and Profile Manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager)** Microsoft Intune role
:::column-end:::
:::row-end:::

## Create an iOS/iPadOS email profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**:

    :::image type="content" source="./media/quickstart-email-profile/ios-create-profile.png" alt-text="Screenshot of Devices section in Intune admin center, Configuration selected, and Create button visible for new policy setup." lightbox="./media/quickstart-email-profile/ios-create-profile.png":::

3. Enter the following properties:

   - **Platform**: Select **iOS/iPadOS**.
   - **Profile type**: Select **Templates** > **Email**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile. For this example, enter **iOS require work email**.
   - **Description**: Enter **Require iOS/iPadOS devices to use work email**.

   :::image type="content" source="./media/quickstart-email-profile/ios-email-profile-name.png" alt-text="Screenshot of Microsoft Intune admin center, Basics step for iOS email profile with Name and Description entered." lightbox="./media/quickstart-email-profile/ios-email-profile-name.png":::

6. Select **Next**.

7. In **Configuration settings**, enter the following settings. For the other settings, use the default values.

   - **Email server**: For this evaluation step, enter `outlook.office365.com`. This setting specifies the Exchange location (URL) of the email server that the iOS/iPadOS mail app uses to connect to email.
   - **Account name**: Enter **Company Email**.
   - **Username attribute from Microsoft Entra ID**: This name is the attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the username for this profile using this name. For this evaluation step, use the **User Principal Name** as the username for the profile, like `user1@contoso.com`.
   - **Email address attribute from Microsoft Entra ID**: This setting is the email address from Microsoft Entra ID that signs in to Exchange. For this evaluation step, select **User Principal Name**.
   - **Authentication method**: For this evaluation step, select **Username and password**. If you set up [authentication certificates in Intune](../protect/certificates-configure.md), then you can choose **Certificate**.

8. Select **Next**.

9. In **Scope tags** (optional), select **Next**. In this example, don't use scope tags.

10. In **Assignments**, use the drop-down for **Assign to** and select **All users and all devices**. Then, select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned.

## Clean up resources

If you don't use this profile for other tutorials or testing, delete it:

1. In the Intune admin center, select **Devices** > **Manage devices** > **Configuration**.
2. Select the **iOS/iPadOS require work email** profile you created, and then select **Delete**.

## Next steps

In this article, you created an email profile for iOS/iPadOS devices. To learn more about all the profiles you can create in Intune, see [Create device profiles in Microsoft Intune](device-profiles.md).

This article is the last step in the evaluation guide. You set up a test environment and stepped through common tasks that help you better understand and use Intune.

When you're ready to deploy Intune in your organization, the following resources can help.

> [!div class="nextstepaction"]
> [Microsoft Intune planning guide](../fundamentals/intune-planning-guide.md)

> [!div class="nextstepaction"]
> [Deploy or move to Microsoft Intune](../fundamentals/get-started-with-intune.md)

> [!div class="nextstepaction"]
> [Migration guide: Set up or move to Microsoft Intune](../fundamentals/deployment-guide-intune-setup.md)
