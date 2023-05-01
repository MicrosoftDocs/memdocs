---
title: Admin checklist for Android software updates in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for Android devices using Microsoft Intune. See tasks and settings that can manage updates on corporate owned Android Enterprise devices.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/26/2023
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: ahamil, talima, brenduns
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Software updates admin checklist for managed Android Enterprise devices in Microsoft Intune

Patches, major & minor updates, and new operating system versions are released frequently. Organizations must keep devices updated to get the latest security updates.

Devices with Android Google Mobile Services (GMS) include all the Google apps and services. These apps and services are on top of the OEMs own firmware features and apps. These devices receive a different type of updates and they're updated randomly, depending on the behaviors by Google, the OEM, and the service carriers/telecommunication company.

Intune has built-in policies that can manage software updates.

This article includes an admin checklist for enrolled and managed Android Enterprise devices. Use this information to help manage software updates on your organization-owned devices.

This article applies to:

- Android Enterprise

> [!TIP]
> If your devices are personally owned, then go to the [software updates admin checklist for personal devices](software-updates-guide-personal-byod.md).

?? Do we need the following information? This article doesn't include any additional info on these different types.??
[tania] this was here just for consistency with the other platforms, we can remove

- **1:1**: Devices are used by only one person.
- **Shared**: Devices are used by more than one person.
- **Dedicated**: Devices are used for a specific business purpose, like a kiosk or digital signage. Not assigned to a specific user.

## Before you begin

To avoid delays in devices receiving updates, make sure devices are:

- Powered on
- Plugged in
- Connected to the Internet
- Idle ??Can we expand on this? By idle, do we mean not running any apps? Or, not currently being used by users/customers? [tania] not being actively used by a user

## Admin checklist for corporate devices

Corporate or organization-owned devices should be enrolled and managed by the organization. For Android Enterprise, you can manage software updates on the following device types:

- Dedicated devices
- Fully managed devices
- Fully managed devices with a work profile

This section lists the Microsoft-recommended policies to install software updates on managed Android devices.

### ✔️ Manage updates with policies

??This section is also in the iOS article version. We can remove it if you like. I added it so there was consistency.??
[tania] this one we should keep because it also applies to Android and for consistency

It's recommended you create policies that update your devices. It's not recommended to put this responsibility on end users.

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.

- Users can apply updates that your organization hasn't approved. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.

- Users can avoid applying required updates that affect security or app compatibility. This situation can leave the devices at risk and/or prevent the devices from functioning.

### ✔️ Configure the system update setting

For enrolled Android Enterprise devices, you can manage OS updates using the **System update** setting. This setting is configurable in an Intune device restrictions configuration profile.

When you configure this setting, you choose when the updates are installed. For example, you can:

- Use the device's default behavior, which automatically installs updates if the device is connected to Wi-Fi, is charging, and is idle.
- Automatically install updates without user interaction. Pending updates install immediately.
- Postpone updates for 30 days and then prompt users to install updates. Expect your device manufacturer and/or carrier to prevent important security updates from being postponed.
- Create a maintenance window to automatically install updates during a specific time frame.

  :::image type="content" source="./media/software-updates-guide-android/system-update-maintenance-window.png" alt-text="Screenshot that shows the system update setting with a maintenance window for Android Enterprise devices in the Microsoft Intune admin center.":::

??Possibly replace image with all options for **System Update** setting, not just the Maintenance window option.??
[tania] the only additional setting that is not on this image is the freeze period that is already shown in the section below. 

For more specific information on this setting and the values you can configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md#general).

### ✔️ Use freeze periods during critical times

During critical periods of the year, like holidays and other events, you can configure a freeze period for system updates. During this time, the devices don't receive system updates, security patches, and notifications about pending updates. Users can't manually check for updates:

:::image type="content" source="./media/software-updates-guide-android/android-enterprise-freeze-period-settings.png" alt-text="Screenshot that shows the freeze period start date and end date for Android Enterprise devices in the Microsoft Intune admin center.":::

For more information on this setting, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md#general).

### ✔️ Use OEMConfig for firmware updates

For some rugged Android devices, you can use OEMConfig to configure firmware updates and other settings that are specific to that OEM. If an OEM provides an OEMConfig app, then in Intune, you can deploy the app and configure its settings using a configuration profile.

To see the Intune-supported OEMConfig apps, go to [Supported OEMConfig apps in Microsoft Intune](../configuration/android-oem-configuration-overview.md#supported-oemconfig-apps). Contact the manufacturer for the firmware and other settings available in the configuration schema.

For more information on OEMConfig in Microsoft Intune, go to [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md)

## Upgrade older devices

As of January 7, 2022, the minimum supported versions are:

- Android 8.0 for device management
- Android 9.0 for mobile application management (MAM)

Devices running Android 7.0 or older that are currently enrolled in Intune don't receive updates to the Android Company Portal app or the Intune app. These apps aren't available in the Google Play Store. If these apps were downloaded before this change, then the devices aren't blocked from enrollment. Policies applied to these devices continue to be deployed, but the devices aren't in a supported state.

If you currently have devices running Android 7.0 or older in your organization, then upgrade or replace them. Use the information in this article to help you define an update strategy. Using newer OS versions provide better productivity and security to your users and your organization.

For more version information, go to [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).

## Next steps

- [Software updates admin checklist and scenarios for BYOD and personal devices](software-updates-guide-personal-byod.md)
- [Software updates admin checklist and scenarios for supervised iOS/iPadOS devices](software-updates-guide-ios-ipados.md)
