---
title: Add or configure education settings in Microsoft Intune
description: Use the Take a Test app in a device configuration profile on Windows devices in Microsoft Intune. Create a configuration profile using the Education settings, and enter a test app URL, choose how users sign-in, monitor the screen during the test, and allow or prevent text suggestions during the test.
author: lenewsad
ms.author: lanewsad
ms.date: 06/22/2026
ms.topic: how-to
ms.reviewer: heenamac
---

# Use the Take a Test app on Windows devices in Microsoft Intune

Education profiles in Intune are designed for students to take a test or exam on devices. This feature includes the **Take a Test** app.

The Take a Test app lets you securely administer online tests on your classroom's Windows devices. To set up the Take a Test app, you create a device configuration profile in Intune and configure the secure assessment settings.

After you configure the profile, assign and deploy it to your students.

When the student signs in, the Take a Test app automatically opens with the test you entered. No other apps can run on the device while the test is in progress. [Take tests in Windows](/education/windows/take-tests-in-windows) provides more details on the Take a Test app.

This article lists the steps to create a device configuration profile in Microsoft Intune. It also lists and describes the available settings for your Windows devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - Windows
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To configure this policy and start collecting inventory data from devices, use an account with at least one of the following roles:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

## Create a device profile

1. Sign in to the [Microsoft Intune admin center].
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Secure assessment (Education)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, enter the settings you want to configure:

    - **Account type**: Choose how users sign in to the test. Your options:
      - Azure AD account (Microsoft Entra account)
      - Domain account
      - Local account
      - Local guest account
    - **Account user name**: Enter the user name of the account used with the Take a Test app. You can enter accounts in the following format:
      - `user@contoso.com`
      - `domain\username`
      - `user@contoso.com`
      - `computerName\username`
    - **Account name**: To set up a local guest account type, enter the name of the account used with the Take a Test app. The account name will appear as a tile on the sign-in screen. Students click the tile to launch the test.​
    - **Assessment URL**: Enter the URL of the test you want users to take. For more information on getting the URL, see the [Take a Test documentation](/education/windows/take-tests-in-windows).
    - **Printer connection**: **Require** only allows access to the Take a Test app from devices that are connected to a printer. This setting also makes the app's print button available to test-takers. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS may allow students to access the app from devices that aren't connected to a printer.​
    - **Screen monitoring**: **Allow** monitors the screen activity while users are taking a test. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS may prevent you from monitoring the screen during the test.
    - **Text suggestions**: Choose **Allow** so test takers can see text suggestions. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS may block text suggestions while users are taking a test.

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../../fundamentals/role-based-access-control/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](../assign-device-profile.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Related content

After the [profile is assigned](../assign-device-profile.md), [monitor its status](../monitor-device-profile.md).

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431