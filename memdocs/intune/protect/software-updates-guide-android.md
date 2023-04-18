---
title: Admin checklist for Android software updates in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for Android devices using Microsoft Intune. See sample policy for different industry scenarios, including shared devices, kiosk, manufacturing, and information worker.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/17/2023
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

# Software updates admin checklist for Android Enterprise devices in Microsoft Intune

In today's rapid pace of modern device management, patches, major and minor updates, and new operating system versions are released frequently. Keeping your devices up to date is incredibly important for many reasons, namely security, compatibility, and new functionality. Microsoft Intune helps you structure and plan your update management strategy for Android.

Android GMS (Google Mobile Services) devices include all the Google Apps and services on top of the OEMs own firmware set of features and flavor. These devices receive different type of updates more or less frequently depending on a series of factors and players, including Google, OEM, and Carriers/Telcos.

This article will help you better understand how Android GMS devices updates work, how important it is to plan and roll out updates, and how Microsoft Endpoint Manager can help with that. 

This article applies to:

- Android Enterprise

## Scenarios - TO DO

Most Android use cases in organizations fall into one of the following scenarios:  

- Personal/BYOD (Android Enterprise Personally Enabled, Mobile Application Management)
- Android Enterprise Corporate (Dedicated, Fully Managed, Fully Managed with a Work Profile)

  - **1:1**: Devices are used by only one person.
  - **Shared**: Devices are used by more than one person.
  - **Dedicated**: Devices are used for a specific business purpose, like a kiosk or digital signage. Not assigned to a specific user.

Typically, organizations also have devices that require the following: 

- OEM Config
- Over-the-air (OTA) updates

We'll get into details for each of scenarios mentioned throughout this article.

Streamlining disruption 

To avoid delays in devices receiving updates, make sure devices are frequently: 

- Connected to Wi-Fi
- Charging
- The device is idle

## Admin checklist for BYOD and personal devices

It's normal for users to not enroll their personal devices in Intune. These devices are considered unmanaged.

By default, when a new update is available for unmanaged devices, users receive notifications and/or see the latest updates available on their devices (Settings > Software Updates). The timing of these updates varies depending on the carrier, OEM, and the device itself. At anytime, users can check for updates themselves.

To control the OS versions on unmanaged devices, there are Intune policies available.

This section lists the Microsoft-recommended policies to install software updates on unmanaged Android devices.

### ✔️ **Create enrollment restrictions**

Users can enroll their personal Android Enterprise devices in Microsoft Intune. When they enroll, these personal or bring-your-own-devices (BYOD) automatically get a work profile. Any policies you create apply to the work profile.

It's recommended to create an enrollment restrictions policy that requires a minimum and maximum operating system version. This policy helps create a good baseline for new enrollments:

:::image type="content" source="./media/software-updates-guide-android/android-enrollment-restrictions-policy.png" alt-text="Screenshot that shows enrollment restrictions policy for Android devices in the Microsoft Intune admin center.":::

When they enroll their personal devices, this policy will check the version info. If the devices is outside the versions you enter, then they're prevented from enrolling. ??Is this true? Not sure if CA (?) is built-in to enrollment restrictions policies??

For more information on this feature, go to [Device platform restrictions in Intune](../enrollment/create-device-platform-restrictions.md).

### ✔️ **Create compliance policies**

Compliance policies are a great tool to help keep devices up-to-date. If a device isn't using a version you define, then the device is marked as noncompliant. Noncompliant devices are shown in the Microsoft Intune admin center.

It's recommended to create compliance policies, and use the built-in reporting to see noncompliant devices & the individual settings that aren't compliant.

In your compliance policy, you can:

- Notify the user that the OS version doesn't meet your requirements
- Allow a grace period before the device is marked non-complaint, to allow them time to upgrade

:::image type="content" source="./media/software-updates-guide-android/compliance-policy-actions-noncompliance.png" alt-text="Screenshot that shows a compliance policy with actions for noncompliance in the Microsoft Intune admin center.":::

If you combine your compliance policies with Conditional Access (CA), then you can block users from resource access until they meet the OS version requirements.

For more information on compliance policies, go to:

- [Create a compliance policy in Microsoft Intune](create-compliance-policy.md)
- [Configure actions for noncompliant devices in Intune](actions-for-noncompliance.md)
- [Monitor results of your compliance policies](compliance-policy-monitor.md)

### ✔️ **Use app protection policies**

On unmanaged personal devices that access organization resources, it's recommended to use app protection policies.

At the app level, you can use app protection policies to determine the minimum OS and patch versions.

When users open or resume an app that's managed by you, the app protection policy can prompt users to upgrade the OS. In the policy, if the version they're running doesn't met your requirements, then you can warn users that a new OS version is required, or block access:

:::image type="content" source="./media/software-updates-guide-android/app-protection-policy-device-conditions.png" alt-text="Screenshot that shows device-based conditions in an app protection policy in the Microsoft Intune admin center.":::

### ✔️ **Use custom notifications**

You can create a custom notification to alert users of upcoming OS version requirements. Use this feature to proactively update their devices so they don't lose access:

:::image type="content" source="./media/software-updates-guide-android/custom-notification.png" alt-text="Screenshot that shows a custom notification message in the Microsoft Intune admin center.":::

Remember, if the OS updates can't be forced or controlled, which is common on personal devices, then end users need to upgrade their own devices.

For more information on these features, go to:

- [Conditional launch actions with app protection policies in Intune](../apps/app-protection-policies-access-actions.md)
- [Using custom notifications in Intune](../remote-actions/custom-notifications.md#considerations-for-using-custom-notifications)

## Admin checklist for corporate devices

Corporate or organization-owned devices should be enrolled and managed by the organization. For Android Enterprise, you can manage software updates on the following device types:

- Dedicated devices
- Fully managed devices
- Fully managed devices with a work profile

This section lists the Microsoft-recommended policies to install software updates on managed Android devices.

### ✔️ Manage updates with policies

??This section is also in the iOS version. We can remove it if you like. I added it so there was consistency.??

It's recommended you create policies that update your devices. It's not recommended to put this responsibility on end users.

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.

- Users can apply updates that your organization hasn't approved. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.

- Users can avoid applying required updates that affect security or app compatibility. This situation can leave the devices at risk and/or prevent the devices from functioning.

### ✔️ Configure the system update setting

For enrolled Android Enterprise devices, you can manage OS updates using the **System update** setting. This setting is configurable in an Intune device restrictions configuration profile.

When you configure this setting, you choose when the updates are installed. For example, you can:

- Use the device's default behavior, which automatically installs updates if the device is connected to Wi-Fi, is charging, and is idle.
- Automatically install updates without user interaction. Pending updates immediately install.
- Postpone updates for 30 days and then prompts users to install updates. Expect your device manufacturer and/or carrier to prevent important security updates from being postponed.
- Create a maintenance window to automatically install updates during a specific time frame.

:::image type="content" source="./media/software-updates-guide-android/system-update-maintenance-window.png" alt-text="Screenshot that shows the system update setting with a maintenance window for Android Enterprise devices in the Microsoft Intune admin center.":::

For more specific information on this setting and the values you can configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md#general).

### ✔️ Use freeze periods during critical times

During critical periods of the year, like holidays and other events, you can configure a freeze period for system updates. During this time, the devices don't receive system updates, security patches, and notifications about pending updates. Users can't manually checking for updates:

:::image type="content" source="./media/software-updates-guide-android/android-enterprise-freeze-period-settings.png" alt-text="Screenshot that shows the freeze period start date and end date for Android Enterprise devices in the Microsoft Intune admin center.":::

For more information on this setting, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md#general).

### ✔️ Use OEMConfig for firmware updates

For some rugged Android devices, you can use OEMConfig to configure firmware updates and other settings that are specific to that OEM. If an OEM provides an OEMConfig app, then in Intune, you can deploy the app and configure its settings using a configuration profile.

To see the Intune-supported OEMConfig apps, go to [Supported OEMConfig apps in Microsoft Intune](..configuration/android-oem-configuration-overview.md#supported-oemconfig-apps). Contact the manufacturer for the firmware and other settings available in the configuration schema.

For more information on OEMConfig in Microsoft Intune, go to [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md)

## Upgrade older devices

As of January 7, 2022, the minimum supported versions are Android 8.0 for device management and 9.0 for mobile application management (MAM). Devices running Android 7.0 or older that are currently enrolled in Intune don't receive updates to the Android Company Portal or the Intune app. These apps aren't available in the Google Play Store. If these apps were downloaded before this change, then then devices aren't blocked from enrollment. Policies applied to these devices continue to be deployed, but the devices aren't in a supported state.

If you currently have devices running Android 7.0 or older in your organization, then upgrade or replace them soon. Use the information in this article to help you define an update strategy. Using newer OS versions provide better productivity and security to your users and your organization.

## Next steps

- [Software updates admin checklist and scenarios for iOS/iPadOS devices](software-updates-guide-ios-ipados.md)
