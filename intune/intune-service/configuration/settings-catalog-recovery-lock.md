---
title: Configure Recovery Lock using the settings catalog
description: Add or create settings using the settings catalog to configure Recovery Lock on macOS devices. Use Recovery Lock to help protect your macOS devices against unauthorized reinstallation and wiping. Using Microsoft Intune, you can configure Recovery Lock settings, and deploy these settings to macOS devices in your organization.
ms.author: mandia
author: MandiOhlinger
ms.date: 03/24/2026
ms.topic: how-to

ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
---

# Configure Recovery Lock on macOS devices in Microsoft Intune

Recovery Lock helps protect your macOS devices against unauthorized reinstallation and wiping. When you add a Recovery Lock policy, Intune automatically generates a strong, random password and sets it on the device.

When you configure this feature:

- Users must enter the password to access the recovery partition environment on the device.
- The password is required to update or remove an existing password.
- The password can be reset automatically using a time-based rotation interval.
- Access to the **Startup Options** screen is protected.

Use the Intune [settings catalog](settings-catalog.md) to configure Recovery Lock on your macOS devices. After you configure the policy, assign it to your macOS devices.

After you configure and assign the policy, you can use device actions to rotate the recovery lock passcode.

To learn more about the recoveryOS password and startup security, see [Startup security in macOS](https://support.apple.com/guide/deployment/startup-security-dep5810e849c/1/web/1.0) (opens Apple's website).

This article applies to:

- macOS

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - **macOS 11.5 or later** and use Apple silicon
> - Devices must be enrolled in Intune and supervised.
>
> Recovery Lock isn't available for macOS devices with Intel chips.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To configure this policy in the settings catalog, use an account with at least one of the following roles:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
>
> To run the device actions, use a [custom role](../fundamentals/create-custom-role.md) with the following permissions:
>
> - Remote tasks/Rotate macOS recovery lock password
> - Remote tasks/View macOS recovery lock password
:::column-end:::
:::row-end:::

## Create the Recovery Lock policy

Use the following steps to create a Recovery Lock policy in the settings catalog.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Enable recovery lock**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**, and search for **Recovery Lock**. Select the **Recovery Lock Password** category, select **Select all these settings**, and then close the settings picker.

    :::image type="content" source="./media/settings-catalog-recovery-lock/recovery-lock-category-settings.png" alt-text="Screenshot that shows Recovery Lock settings in the settings catalog in Microsoft Intune and Intune admin center." lightbox="./media/settings-catalog-recovery-lock/recovery-lock-category-settings.png":::

8. Configure the Recovery Lock settings:

    - **Enable Recovery Lock Password**: Select **Enabled** to enable the Recovery Lock feature on the device.

    - **Recovery Lock Password Rotation Schedule**: Enter the number of months before the recovery lock password is automatically reset, from 1 to 12 months.

      When the schedule triggers, Intune updates the password on the device and securely stores it in the Intune admin center.

      Be sure to set a schedule that meets your organization's security requirements. A shorter rotation interval increases security, as it reduces risk if a password is leaked. It can also increase help desk calls if users need to access the recovery partition often.

9. Select **Next**. In **Scope tags**, select **Next**.

    Scope tags are optional, and this example doesn't use them. To learn more about scope tags, and what they do, go to [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

10. In **Assignments**, select **Next**.

    Assignments are optional, and this example doesn't use them. In production, select **Add groups**. Select a Microsoft Entra group that includes users or devices that should receive this policy. For information and guidance on assigning policies, see [Assign user and device profiles in Intune](device-profile-assign.md).

11. In **Review + create**, review the summary of your changes. Select **Create**.

    When you create the profile, your policy is automatically assigned to the users or groups you chose. If you didn't choose any users or groups, then your policy is created, but it isn't deployed.

    In **Devices** > **Configuration**, your new policy is shown in the list.

## Monitor Recovery Lock status and view the password - Still accurate??

When you assign the policy to devices, you can monitor its status.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > select the macOS device.
2. In **Resource explorer**, select **AppleDevicesStates**. Confirm the status in the **Recovery Lock** column.
3. If Recovery Lock is enabled, you can view the password at **Passwords and keys** > **Recovery Lock Password**.

When you unenroll the device from Intune, the Recovery Lock password is automatically cleared from the device.

## Remove or rotate the Recovery Lock password - Still needed? Not sure if this referring to the remove device action??

If you need to service, recover, or transfer a device, you can remove or update the Recovery Lock password.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > select the macOS device.
2. Select **Recovery lock** and then select one of the following options:

    - **Set**: Set the recovery lock password for the devices.
    - **Rotate**: Reset the recovery lock password for the devices.
    - **Clear**: Clear the recovery lock password for the devices.

3. Confirm the action.

## Use the rotate recovery lock passcode device action

You can use the rotate recovery lock passcode device action to reset the recovery lock password on demand. This action is helpful if a user forgets their password, or if you want to proactively rotate the password outside of the rotation schedule you set in the policy.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > select the macOS device.
2. Select **Rotate recovery lock passcode**.
3. Confirm the action.

To learn more, see [Need link from Paolo ??]().

## Related content

- [Use the Intune settings catalog to configure settings](settings-catalog.md)
- [Common tasks you can complete using the settings catalog](settings-catalog-common-features.md)
