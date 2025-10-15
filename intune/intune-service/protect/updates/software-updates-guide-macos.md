---
title: "Admin Guide: Manage macOS Updates with Intune"
description: Learn how to manage macOS software updates with Microsoft Intune. Create policies, control update timing, and monitor update status for organization-owned devices.
author: paolomatarazzo
ms.author: paoloma
ms.date: 10/15/2025
audience: ITPro
ms.topic: how-to
ms.reviewer: beflamm, ahamil, rogerso
ms.collection:
- M365-identity-device-management
- sub-updates
---

# Software updates planning guide for managed macOS devices in Microsoft Intune

Keeping your devices current with updates is critical. Admins must do what they can to reduce risk of security events, and reduce this risk with minimal disruption to the business & users.

Intune has built-in policies that can manage software updates. For macOS devices, you can use Intune to manage device updates, configure when devices are updated, and review the device update status.

Use this article as an admin guide for your enrolled and managed macOS devices. This information can help you manage software updates on your organization-owned devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> The configuration of Software Update for Apple devices requires the following platforms:
>
> - macOS 14.0 and later
:::column-end:::
:::row-end:::

> [!TIP]
>
> - If your devices are personally owned, then go to the [software updates admin guide for personal devices](../software-updates-guide-personal-byod.md).
> - [!INCLUDE [Apple MDM software updates deprecation](../../includes/apple-mdm-updates-deprecation.md)]

### Before you begin

To install updates faster and avoid delays, make sure the devices are:

- Powered on; not shut down but can be can a sleep state
- Plugged in
- Connected to Internet

## ✅ Manage updates with policies

Microsoft recommends creating policies that update your devices.

By default, users receive notifications and/or see the latest updates available on their devices (Settings > General > Software Updates). Users can choose to download and install updates whenever they want.

:::row:::
:::column span="3":::
They can also change the update behavior using the Automatic Updates feature on the device (Settings > Software Updates):
:::column-end:::
:::column span="1":::
:::image type="content" source="images/default-update-settings-macos-device.png" alt-text="The operating system default update settings and controls on a macOS Apple device.":::
:::column-end:::
:::row-end:::

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can apply updates that your organization hasn't approved. This situation can cause issues with application compatibility, or changes to the operating system or user experience that disrupt device use.
- Users can avoid applying updates that are required for security or app compatibility reasons. This delay can leave the devices at risk and/or prevent them from being able to function.
- Users can disable checking for new updates entirely.

Because of these potential issues, Microsoft recommends that you evaluate your use case scenarios and deploy policies to manage the update experience to minimize risk and disruption to your business.

## Admin checklist for organization owned devices

To update macOS devices owned by your organization, Microsoft recommends the following features. You can also use these features as a starting point for your own update strategy.

### ✅ Use DDM-managed software updates

Use Apple's declarative device management (DDM) to install a specific update by an enforced deadline.

DDM is the modern way to manage settings. The independent nature of DDM provides an improved user experience, as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads the update, prepares the device for the installation, and installs the update.

Don't use the MDM-based software update policy settings on these devices, as Apple deprecated the MDM policies.

The DDM settings are configurable in the [Intune settings catalog](../../configuration/settings-catalog.md). For more information, go to [Configure update policies for Apple devices](apple.md).

<!--
### ✅ Use MDM on macOS 13 and older

On macOS versions 13 and older, you can use Apple's MDM settings built-in to Intune. For these devices, you create two policies that work together to manage the update experience. The first policy manages when updates are installed, and the second policy manages how updates are installed.

#### Step 1 - Use a software update policy to manage when updates are installed

In a software update policy, you can manage when critical updates and firmware updates are installed. You can also manage how many times the user can defer an update before it's force installed. Depending on the settings you enter, users aren't prompted and don't need to be using the device when the updates are installed.

For most organizations, Microsoft recommends you configure the settings available in a [software update policy](software-updates-macos.md).

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Apple updates > macOS update policies**.
1. Configure the following settings:

    - **Update policy behavior settings**

      - **Critical updates**: Install later
      - **Firmware updates**: Install later
      - **Configuration file updates**: Install later
      - **All other updates (OS, built-in apps)**: Install later
        - **Maximum user deferrals**: 5
        - **Priority**: High

      > [!NOTE]
      >
      > - On recent macOS builds, almost all updates show as **Configuration data files** or **All other updates**. The **All other updates** settings are mostly legacy updates for older builds of macOS.
      > - The time specified in these settings is used by the Intune service. The time isn't the local device time. Be aware of time differences when you configure a maintenance window, especially for a global environment.

    - **Update policy schedule settings**

      - **Schedule type**: Update at next check-in

      You can change the values to your preferred scheduled times. Some of the values might only affect minor updates, and not major updates.

For the specific steps, and more information on these settings & their values, go to [Manage macOS software update policies in Intune](software-updates-macos.md).

##### End user experience

With these settings, this policy locks these settings so users can't change them. The policy also:

1. Checks for updates each time the device checks in with the Intune service. If there are updates available, then they're automatically downloaded.

2. The device finds a time period when the device isn't being used.

    - If the device isn't being used, then the policy tries to automatically install the update.
    - If the device is being used, then end users can choose to install the update, or defer the installation up to five times. Be sure to encourage your end users to install updates when they're available.

    The following images show the prompts that end users can see when updates are available:

    :::image type="content" source="images/required-managed-update-sample-notification-macos.png" alt-text="The sample notification prompt for a required update on a macOS Apple device.":::

    :::image type="content" source="images/updates-available-sample-notification-macos.png" alt-text="The sample notification that an update is available on a macOS Apple device.":::

3. If end users use all the deferrals, then the update is force installed. For a forced installation, a restart doesn't prompt the end user, and could result in data loss.

#### Step 2 - Use a settings catalog policy to manage how updates are installed

The [Intune settings catalog](../../configuration/settings-catalog.md) includes settings to help manage software updates. In this step, you create a policy that:

- Configures the device to automatically install updates when they're available, including app updates.
- Prevents end users from disabling update checks.
- Configures the device to check for updates and prompt users regularly.

This settings catalog policy works with [Step 1 - Use a software update policy to manage when updates are installed](#step-1---use-a-software-update-policy-to-manage-when-updates-are-installed) (in this article). It makes sure the devices are checking for updates and prompting users to install them. End users still need to take action to finish the installation.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Manage devices > Configuration > Settings catalog > Software Update**.
1. Configure the following settings:

    - **Allow Pre Release Installation**: False
    - **Automatic Download**: True
    - **Automatically Install App Updates**: True
    - **Critical Update Install**: True
    - **Restrict Software Update Require Admin To Install**: False
    - **Config Data Install**: True
    - **Automatically Install MacOS Updates**: True
    - **Automatic Check Enabled**: True

For more information on the settings catalog, including how to create a settings catalog policy, go to [Use the settings catalog to configure settings](../../configuration/settings-catalog.md).

##### End user experience

This policy locks these settings so users can't change them. On the device, the software update settings are greyed out:

:::image type="content" source="images/update-settings-with-settings-catalog-policy-macos.png" alt-text="The software update settings are greyed out after the Intune settings catalog update policy applies to a macOS Apple device.":::

-->

## ✅ Consider using the Nudge community tool

This tool is optional, and can help you **manage the end user experience**.

A popular tool within the Microsoft macOS admin community is Nudge. [Nudge is an open source community tool](https://github.com/macadmins/nudge) that encourages end users to install macOS updates. It provides a rich configuration experience for admins.

When Nudge is configured and deployed, end users see the following sample message when their device is ready to be updated. End users can also choose to update the device or defer the update:

:::image type="content" source="images/nudge-sample-notification-message-macos.png" alt-text="A sample Nudge community tool message when a software update is available a macOS Apple device." lightbox="images/nudge-sample-notification-message-macos.png":::

There's also a [sample script and Intune configuration policy](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Apps/Nudge) for Nudge in the Microsoft shell script repository. This script includes everything you need to get started with Nudge. Make sure you update the `.mobileconfig` file with your values.

## ✅ Use built-in reporting for update status

After the update policies are deployed, in the Intune admin center you can use different reports to monitor the update status of your managed Apple devices.

For more information, see [View Software Update Reports for Apple Devices](apple-reports.md).

## Related articles

- [Software updates planning guide for BYOD and personal devices in Microsoft Intune](../software-updates-guide-personal-byod.md)
- [Software updates planning guide for managed Android Enterprise devices in Microsoft Intune](../software-updates-guide-android.md)
- [Software updates planning guide and scenarios for supervised iOS/iPadOS devices in Microsoft Intune](software-updates-guide-ios-ipados.md)
