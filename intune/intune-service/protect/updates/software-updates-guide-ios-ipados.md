---
title: "Admin Guide: Manage iOS/iPadOS Updates with Intune"
description: Learn how to manage iOS/iPadOS software updates in Microsoft Intune with this admin checklist. Explore policies for shared, kiosk, and industry-specific devices.
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


# Software updates planning guide and scenarios for supervised iOS/iPadOS devices in Microsoft Intune

Keeping your mobile devices current with software updates is critical. You need to reduce the risk of security events and have minimal disruption to your organization and your users. On iOS/iPadOS supervised devices, Intune has built-in policies that can manage software updates.

This article includes an admin checklist to help you get started with software updates on iOS/iPadOS supervised devices. It also lists common industry scenarios and sample policies that you can configure in your environment.

For the specific steps to create a software update policy, see [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> The configuration of Software Update for Apple devices requires the following platforms:
>
> - iOS/iPadOS 17.0 and later
:::column-end:::
:::row-end:::

> [!TIP]
>
> - If your devices are personally owned, then go to the [software updates planning guide for personal devices](../software-updates-guide-personal-byod.md)
> - [!INCLUDE [Apple MDM software updates deprecation](../../includes/apple-mdm-updates-deprecation.md)]

## Admin checklist for organization owned devices

This section lists the Microsoft-recommended guidance and strategies to install software updates on your devices.

### ✅ Manage updates with policies

Microsoft recommends creating policies that update your devices.

By default, users receive notifications and see the latest updates available on their devices (Settings > General > Software Updates). Users can choose to download and install updates whenever they want.

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.
- Users can apply updates that your organization doesn't approve. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.
- Users can avoid applying required updates that affect security or app compatibility. This situation can leave the devices at risk and prevent the devices from functioning.

### ✅ Keep automatic updates enabled

Apple devices automatically install updates when they're available. By default, this feature is enabled on new devices. **Keep this feature enabled**.

To use this automatic patching and install updates faster, make sure the devices are:

- Powered on
- Plugged in
- Connected to the Internet

When the devices are powered on, plugged in, and connected to the Internet, the updates automatically download and install, and the device reboots. If the device doesn't meet these conditions, the updates don't automatically download and install.

:::row:::
:::column span="3":::
To keep your devices on the most current version with minimal effort, keep the automatic updates feature enabled:
:::column-end:::
:::column span="1":::
:::image type="content" source="images/apple-automatic-update-settings.png" alt-text="Screenshot that shows automatic update settings on iOS/iPadOS Apple devices." lightbox="images/apple-automatic-update-settings.png":::
:::column-end:::
:::row-end:::

Automatic updates work together with other update policies, which can provide a positive experience for admins and end users.

Using Intune policies, you can also force users to update their devices:

- Use [Enrollment Restrictions](../../enrollment/create-device-platform-restrictions.md) to prevent users from enrolling devices that aren't current.
- Create [compliance policies](../compliance-policy-create-ios.md) to determine the devices that aren't updated.
- Create [Conditional Access (CA) policies](../create-conditional-access-intune.md) to block devices that aren't updated. The CA policies can also prompt users to install current updates so they regain access.

#### What you need to know

- If you disable the automatic updates feature, policies can't change it because of an OS limitation. You must manually change the setting on the device or reset and reprovision the device.
- If you configure devices with a PIN, you must enter the PIN to start the software update. Entering the PIN typically isn't an issue for information worker 1:1 devices.\
  When planning for updates on kiosks, factory floor, or userless scenarios, you might need to adjust your processes to accommodate for the PIN behavior.

### ✅ Use the built-in settings

Use Apple's declarative device management (DDM) to manage software updates. DDM is the modern way to manage devices with an improved user experience, as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads the update, prepares the device for the installation, and installs the update.

The DDM settings are configurable in the [Intune settings catalog](../../configuration/settings-catalog.md). For more information, go to [Configure update policies for Apple devices](apple.md).

<!--
- **Software update policies**

  These MDM policies offer a controlled roll-out of a specific version. You can also force devices on older versions to upgrade. Admins can enter the iOS/iPadOS version to install and schedule the installation.

  You can configure these settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, see [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

- **Software update deferral policies**

  These MDM policies hide updates for up to 90 days. They prevent users from manually updating their device to a version that isn't approved. This feature doesn't control when the updates are applied.

  You can configure these settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, see [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

With these features, admins can make sure their Apple devices run a specific software version and can control the release of updates across their devices.
-->

### ✅ Create policies that support many time zones

All policy times use Coordinated Universal Time (UTC). The device's local time zone isn't used.

To minimize the number of policies you need to create and manage, create a configuration that supports many time zones. Don't create a separate policy for each time zone.

For example, in the United States, there are four primary time zones: Pacific (UTC-8), Mountain (UTC-7), Central (UTC-6), and Eastern (UTC-5). You can create separate policies for each time zone. Or, create one or two policies that achieve the same result.

### ✅ Be careful with version settings

When you create software update policies, be aware of the broader effect of the version details in all your policies.

For example:

- You configure a policy that delays updates for 90 days. If an enrollment restriction policy requires devices to have a recent iOS/iPadOS version, then after a device reset, devices could be blocked from enrolling.

- You create a compliance policy that requires a minimum iOS/iPadOS version that's recent. With this policy, devices on older releases become noncompliant. If you use Conditional Access to enforce compliance, then users are blocked and can't work.

## Common industry scenarios

Apple devices are used in various industries, including enterprise, retail, manufacturing, and education. Most device use cases fall into the following categories:

- **1:1**: One person uses the device.
- **Shared**: More than one person uses the device.
- **Dedicated**: The device serves a specific business purpose, such as a kiosk or digital signage.

The following table lists common industry terminology used in this article:

| Industry | Terminology | Use case |
| --- | --- | --- |
| Enterprise | Knowledge worker | 1:1 |
| Retail | Kiosk  | Dedicated |
| Manufacturing | Factory machine | Mission critical |
| Education | Assigned device | Shared |

This section describes some common industry scenarios and gives examples of Intune policies.

### Knowledge workers

This group includes people with specialized knowledge who work in enterprise businesses and organizations. Their knowledge and thinking ability are central to their jobs. Some examples include engineers, content developers, programmers, accountants, communications specialists, consultants, and so on.

Knowledge workers typically have their own device. They don't share their device with other users or other knowledge workers.

In scenarios like knowledge worker devices, the primary goal is for the update process to be as simple and quick as possible. Their apps are mostly store-based, and the apps should remain compatible with the latest OS version. On these devices, users are typically tolerant of prompts for updates and choosing a convenient time for reboots.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> - Basic update configuration
> - The latest most up-to-date version
> - Automatic updates

**Scenario example**:

You're configuring an update profile for the knowledge workers at Contoso. These users mostly use Microsoft 365 apps and several Volume Purchase Program (VPP) apps.

As an admin, you're comfortable with:

- These devices running the latest released iOS/iPadOS version
- Downloading and installing updates as soon as the devices check in with Intune
- Allowing end users to decide when they install updates and reboot their devices to apply the updates

To accomplish these goals, use a policy that enforces the latest version.

### Kiosks

These devices are typically in-store retail devices, and they can be a desktop computer or a mobile device. Employees use these devices to serve customers, and customers use them directly for self-service tasks. They can also be a visual display that all customers see when they're on-premises.

In kiosk-like scenarios, the primary goals for updating the devices are:

- Make sure devices are current with approved OS updates.
- Admins manage the updates and any versioning.
- The installation and reboots occur after business hours.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Basic update configuration
> * Predictable version control
> * Predictable release cycles

**Scenario example**:

You're configuring an iOS/iPadOS update profile for the kiosk devices at Contoso. These devices operate in a retail outlet. Your staff uses the devices to serve customers seven days a week, including extended retail hours. The devices run a single Line of Business (LOB) kiosk app, which Contoso developed in-house. This internal application is only tested and validated on a quarterly basis.

You want to deploy the specific iOS/iPadOS version that this LOB app was recently tested with, which is iOS 16.3. If this kiosk application doesn't work correctly, then the retail outlet can't serve customers. The devices connect to Wi-Fi and charge overnight when the retail outlet is closed to customers.

You choose an overnight servicing window of 10 hours where updates can be downloaded and applied, before the store opens.

To accomplish this task, create a policy that enforces a targeted version and a specific installation time.

### Factory machines

These devices are often single-purpose devices. Use them in mission critical areas, like manufacturing lines or specialized equipment control and monitoring. For example, it could be an Android tablet running control or monitoring software for a device that welds components.

In factory machine scenarios, the primary goal is to make sure devices behave in a consistent manner. You might need to delay updates so you can complete all application compatibility testing. Installation and reboots occur at specific times and typically deploy in a phased approach.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Advanced policy configuration
> * Strict version control
> * Slow release cycles

**Scenario example**:

You're configuring an update profile for devices on the manufacturing floor at Contoso's industrial facility. The facility runs 24x7, 365 days a year, except for a few hours of mandatory stoppage for safety inspections. These inspections happen early Sunday morning every week.

These devices run two vendor apps. To remain in a supported configuration, you update both apps infrequently and must run a specific version of the app and OS.

You want to deploy a specific, older iOS/iPadOS version (17) to these devices, as the app vendor doesn't support later releases yet. Since the devices are nearly always in use, you only have a small maintenance window once a week on Sunday.

You want to schedule updates during a two hour downtime window overnight on a Sunday.

To accomplish this task, create a policy that enforces a targeted version and a specific installation time.

### Shared devices

Many users use shared devices and typically sign in and out of the device, including in education environments. These devices can be terminal or desktop computers, tablets, laptops, and smartphones. Offices, classrooms, and retail stores often use these devices.

For more information on managing shared iOS/iPadOS devices, see [Shared device solutions for iOS/iPadOS](../../enrollment/device-enrollment-shared-ios.md).

For iOS/iPadOS shared devices, all users must be signed out to apply updates. The users can be signed out or the device can be rebooted, which automatically signs out users.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Advanced policy configuration
> * Predictable version control
> * Controlled update behavior

**Scenario example**:

In the morning, UserA signs in to the device to check email before going out on the floor. An hour later, UserB uses the same device to run some LOB apps.

You need to configure an update for this shared device. General knowledge workers use these shared devices in the office from 8 AM – 5 PM, Monday through Friday. You want the devices on the latest iOS/iPadOS version that supports all the apps used on the shared devices.

To keep the policy as simple as possible, you want the updates to install outside typical working hours, plus one hour for reboots or other actions.

To accomplish this task, this scenario involves two policies:

- In the first policy, you want all users signed out or want to reboot the device after a set amount of time. You can create an Apple Business Manager enrollment profile to sign out any users who are idle for more than 15 minutes (900 seconds):

  :::image type="content" source="images/shared-devices-maximum-seconds-policy-settings.png" alt-text="Screenshot that shows how to enroll iOS/iPadOS devices without user affinity and setting the inactivity value in the Microsoft Intune admin center." lightbox="images/shared-devices-maximum-seconds-policy-settings.png":::

- In the second policy, schedule the update using the following settings:

  :::image type="content" source="images/shared-devices-outside-scheduled-time-policy-settings.png" alt-text="Screenshot that shows installing the latest version and outside scheduled time software update settings for iOS/iPadOS devices in the Microsoft Intune admin center." lightbox="images/shared-devices-outside-scheduled-time-policy-settings.png":::

## Related articles

- [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md)
- [Software updates planning guide and scenarios for BYOD and personal devices](../software-updates-guide-personal-byod.md)
- [Software updates planning guide for managed Android devices](../software-updates-guide-android.md)
- [Software updates planning guide for managed macOS devices](software-updates-guide-macos.md)
