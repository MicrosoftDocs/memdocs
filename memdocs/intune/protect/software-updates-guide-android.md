---
title: Admin checklist for Android software updates in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for Android devices using Microsoft Intune. See sample policy for different industry scenarios, including shared devices, kiosk, manufacturing, and information worker.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/12/2023
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

## Scenarios

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

By default, when a new update is available for unmanaged devices, users receive notifications and/or see the latest updates available on their devices (Settings > Software Updates). The timing of these updates varies depending on the carrier, OEM, and the device itself.

To control the OS versions on unmanaged devices, there are other Intune policies available.

This section lists the Microsoft-recommended policies to install software updates on unmanaged Android devices.

### ✔️ **Create enrollment restrictions**

Users can enroll their personal Android Enterprise devices in Microsoft Intune. When they enroll, these personal or bring-your-own-devices (BYOD) automatically get a work profile. Any policies you create apply to the work profile.

It's recommended to create an enrollment restrictions policy that requires a minimum and maximum operating system version. When they enroll their personal devices, the

:::image type="content" source="./media/software-updates-guide-android/android-enrollment-restrictions-policy.png" alt-text="Screenshot that shows enrollment restrictions policy for Android devices in the Microsoft Intune admin center.":::

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

On personal devices that access organization resources, it's recommended to use app protection policies.

At the app level, you can use app protection policies to determine the minimum OS and patch versions.

When users open or resume an app that's managed by you, the app protection policy can prompt users to upgrade the OS. In the policy, if the version they're running doesn't met your requirements, then you can warn the user, or block access:

:::image type="content" source="./media/software-updates-guide-android/app-protection-policy-device-conditions.png" alt-text="Screenshot that shows device-based conditions in an app protection policy in the Microsoft Intune admin center.":::

If the OS updates can't be forced or controlled, which is common on personal devices, then end users need to upgrade their own devices.You can create a custom notification to alert users of upcoming OS version requirements and guide them to proactively update so they don't lose access:

:::image type="content" source="./media/software-updates-guide-android/custom-notification.png" alt-text="Screenshot that shows a custom notification message in the Microsoft Intune admin center.":::

For more information on these features, go to:

- [Conditional launch actions with app protection policies in Intune](../apps/app-protection-policies-access-actions.md)
- [Using custom notifications in Intune](../remote-actions/custom-notifications.md#considerations-for-using-custom-notifications)

## Admin checklist for corporate devices

- Dedicated
- Fully Managed
- Fully Managed with a work profile

### ✔️ Manage updates with policies

It's recommended you create policies that update your devices. It's not recommended to put this responsibility on end users. 

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.

- Users can apply updates that your organization hasn't approved. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.

- Users can avoid applying required updates that affect security or app compatibility. This situation can leave the devices at risk and/or prevent the devices from functioning.

### ✔️ Configure the system update setting

For Android Enterprise Dedicated, Fully Managed and Corporate-Owned with a Work Profile, you can manage operating system updates via a Device Restrictions configuration profile by configuring the "System update" setting. You can choose from the following options. 

- **Device default** – default behavior is to update automatically if the device is connected to wi-fi, is charging and is idle. For app updates, it also validates if the app is not running in the foreground.  

- **Automatic** – updates are automatically installed without user interaction. When choosing this option, any pending updates will be installed immediately.  

- **Postponed** – postpones updates for 30 days, after that time, users are prompted to install the update. However, device manufacturers and carriers can exempt important security updates from being postponed. If that happens, the user will see a system notification on the device. 

- **Maintenance window** – updates are installed automatically within a maintenance window you define. If certain conditions are not met (insufficient space or battery levels, for example) it keeps trying daily for 30 days. After that time, the user is prompted to install the update. If you're using dedicated devices, such as kiosks or digital signage, you may want to consider this option as single-app foreground apps can be updated. This setting is valid for both operating system and app updates. Maintenance windows takes precedence over the device being changed.

### ✔️ Add a freeze period

Optionally, you can also configure freeze periods for system updates, up to a maximum of 90 days. This setting allows to specific a start and end date for updates during critical periods of the year (like holidays and other events). When you specify this setting, during that time frame, the device will not receive system updates, security patches or notifications about pending updates. Manually checking for updates is also unavailable. There's a mandatory period of 60 days you can set between freezes. This is for security reasons,  to avoid the device from being under update freeze indefinitely. The freeze period settings requires Android 9.0 and newer.

:::image type="content" source="./media/software-updates-guide-android/android-enterprise-freeze-period-settings.png" alt-text="Screenshot that shows the freeze period start date and end date for Android Enterprise devices in the Microsoft Intune admin center.":::

[General Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work#general.md)

### ✔️ Use OEMConfig for firmware updates

For some rugged Android devices, you may also leverage OEMConfig to configure firmware updates, among other settings that are specific to that OEM. If an OEM provides an OEMConfig app, you may deploy the apps and the configuration profile from Intune. To see what OEMConfig apps are supported today in Microsoft Intune, refer to this doc. To confirm what firmware and other settings are available in the configuration schema from a specific OEM, please reach out to the manufacturer.

[Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md)

## Upgrade older devices

In January 7, 2022 we moved to support Android 8.0 for device management and 9.0 for MAM as the minimum supported versions. Devices running Android 7.0 or below that are currently enrolled in Intune will not receive updates to the Android Company Portal or the Intune app moving forward. These apps will no longer be available in the Google Play Store, however, if they were downloaded prior to this change, the devices will not be blocked from enrolment. Policies applied to those devices will continue to be deployed however the devices will no longer be in a supported state.     

If you currently have devices running Android 7.0 or below in your organization, plan to upgrade or replace them soon. Use the information on this article to help you define an update strategy. Leveraging newer OS versions will provide better productivity and security to your users and your organization.

## Next steps

- [Software updates admin checklist and scenarios for iOS/iPadOS devices](software-updates-guide-ios-ipados.md)
