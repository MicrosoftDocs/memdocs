---
title: Create an email device profile for iOS/iPadOS devices
description: Learn how to use Microsoft Intune to create an email device profile so iOS/iPadOS devices can securely connect to company organization email.
author: MandiOhlinger
ms.author: mandia
ms.date: 08/14/2024
ms.topic: how-to
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
---

# Step 11: Create an email device profile for iOS/iPadOS

This article is part of a series that walks you through common Intune tasks. In this article, you create an email profile for iOS/iPadOS devices.

The profile includes the required settings that allow a device to connect to your organization email. Email device profiles help standardize settings across your devices. And, they can also let end users access organization email on their personal devices without any confusing setup.

To help safeguard your email, you can use an email profile to determine if devices are compliant. Then, set up Conditional Access to allow only compliant devices access to email. For details about email profiles, go to [How to configure email settings in Microsoft Intune](email-settings-configure.md)

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Sign in to Intune

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as the built-in **[Policy and Profile Manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager)** Intune role.

If you created an Intune Trial subscription, the account that created the subscription is a Microsoft Entra [Global Administrator](/entra/identity/role-based-access-control/permissions-reference#global-administrator).

> [!CAUTION]
> [!INCLUDE [global-admin](../includes/global-admin.md)]

## Create an iOS/iPadOS email profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**:

    :::image type="content" source="./media/quickstart-email-profile/ios-create-profile.png" alt-text="Create a new device configuration profile in Microsoft Intune using the Intune admin center.":::

3. Enter the following properties:

   - **Platform**: Select **iOS/iPadOS**.
   - **Profile type**: Select **Templates** > **Email**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile. For this example, enter **iOS require work email**.
   - **Description**: Enter **Require iOS/iPadOS devices to use work email**.

   :::image type="content" source="./media/quickstart-email-profile/ios-email-profile-name.png" alt-text="Create an email device configuration profile for iOS/iPadOS devices in Microsoft Intune and Intune admin center.":::

6. Select **Next**.

7. In **Configuration settings**, enter the following settings. For the other settings, use the default values.

   - **Email server**: For this evaluation step, enter `outlook.office365.com`. This setting specifies the Exchange location (URL) of the email server that the iOS/iPadOS mail app uses to connect to email.
   - **Account name**: Enter **Company Email**.
   - **Username attribute from Microsoft Entra ID**: This name is the attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the username for this profile using this name. For this evaluation step, we use the **User Principal Name** as the username for the profile, like `user1@contoso.com`.
   - **Email address attribute from Microsoft Entra ID**: This setting is the email address from Microsoft Entra ID that signs in to Exchange. For this evaluation step, select **User Principal Name**.
   - **Authentication method**: For this evaluation step, select **Username and password**. If you set up [authentication certificates in Intune](../protect/certificates-configure.md), then you can choose **Certificate**.

8. Select **Next**.

9. In **Scope tags** (optional), select **Next**. In this example, we don't use scope tags.

10. In **Assignments**, use the drop-down for **Assign to** and select **All users and all devices**. Then, select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned.

## Clean up resources

If you don't use this profile for other tutorials or testing, then you can delete it:

1. In the Intune admin center, select **Devices** > **Manage devices** > **Configuration**.
2. Select the **iOS/iPadOS require work email** profile you created, and then select **Delete**.

## Next steps

In this article, you created an email profile for iOS/iPadOS devices.

You can use this profile to determine if an iOS/iPadOS device is compliant by creating a compliance policy. If any iOS/iPadOS devices don't match the profile, then the compliance policy marks the device as noncompliant. For more protection, you can create a Conditional Access policy that blocks noncompliant iOS/iPadOS devices from accessing email. For more information about device compliance policies, go to [Get started with device compliance policies in Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Deploy or move to Microsoft Intune](../fundamentals/get-started-with-intune.md)
