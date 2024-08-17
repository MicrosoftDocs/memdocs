---
title: Admin checklist for iOS/iPadOS software updates in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for iOS/iPadOS devices using Microsoft Intune. See sample policy for different industry scenarios, including shared devices, kiosk, manufacturing, and information worker.
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 01/30/2024
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: ahamil, rogerso, mandia
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- sub-updates
---

# Software updates planning guide and scenarios for supervised iOS/iPadOS devices in Microsoft Intune

Keeping your mobile devices current with software updates is critical. You need to reduce the risk of security events and have minimal disruption to your organization and your users. On iOS/iPadOS supervised devices, Intune has built-in policies that can manage software updates.

This article includes an admin checklist to help you get started with software updates on iOS/iPadOS supervised devices. It also lists common industry scenarios and sample policies that you can configure in your environment.

For the specific steps to create a software update policy, go to [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

This article applies to:

- iOS/iPadOS supervised devices enrolled in Intune

> [!TIP]
> If your devices are personally owned, then go to the [software updates planning guide for personal devices](software-updates-guide-personal-byod.md).

## Admin checklist for organization owned devices

This section lists the Microsoft-recommended guidance and strategies to install software updates on your devices.

### ✅ Manage updates with policies

It's recommended you create policies that update your devices. It's not recommended to put this responsibility on end users.

By default, users receive notifications and/or see the latest updates available on their devices (Settings > General > Software Updates). Users can choose to download and install updates whenever they want.

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.

- Users can apply updates that your organization hasn't approved. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.

- Users can avoid applying required updates that affect security or app compatibility. This situation can leave the devices at risk and/or prevent the devices from functioning.

### ✅ Keep automatic updates enabled

Starting with iOS/iPadOS 12, when updates are available, Apple devices automatically install the updates. By default, this feature is enabled on new devices. **Keep this feature enabled**.

To use this automatic patching and install updates faster, make sure the devices are:

- Powered on
- Plugged in
- Connected to the Internet  

When the devices are powered on, plugged in, and connected to the Internet, then the updates automatically download & install, and the device reboots. If the device doesn't meet these conditions, then the updates won't automatically download and install.

To keep your devices on the most current version and with minimal effort from you, keep the automatic updates feature enabled:

:::image type="content" source="./media/software-updates-guide-ios-ipados/apple-automatic-update-settings.png" alt-text="Screenshot that shows automatic update settings on iOS/iPadOS Apple devices.":::

Automatic updates work together with other update policies, which can provide a positive experience for admins and end users.

Using Intune policies, you can also force users to update their devices:

- Use [Enrollment Restrictions](../enrollment/create-device-platform-restrictions.md) to prevent users from enrolling devices that aren't current.
- Create [compliance policies](compliance-policy-create-ios.md) to determine the devices that aren't updated.
- Create [Conditional Access (CA) policies](create-conditional-access-intune.md) to block devices that aren't updated. The CA policies can also prompt users to install current updates so they regain access.

#### What you need to know

- If the automatic updates feature is disabled, then due to an OS limitation, it can't be changed using policies. The setting must be manually changed on the device or the device must be reset & reprovisioned.

- If devices are configured with a PIN, then to start the software update, you must enter the PIN. Entering the PIN typically isn't an issue for information worker 1:1 devices.

  When planning for updates on kiosks, factory floor or userless scenarios, you might need to adjust your processes to accommodate for the PIN behavior.

### ✅ Use the built-in settings

To manage updates, Apple has the following options:

- **Declarative device management (DDM)**

  On iOS/iPadOS 17.0 and later, you can use Apple's declarative device management (DDM) to manage software updates. DDM is a new way to manage devices with an improved user experience, as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

  DDM is the recommended way to manage updates on iOS/iPadOS 17+ devices. You can use MDM settings on these devices, but it's not recommended. Instead, use the DDM settings.

  These settings are configurable in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, go to [Managed software updates with the settings catalog](managed-software-updates-ios-macos.md).

- **Software update policies**

  These MDM policies offer a controlled roll-out of a specific version. You can also force devices on older versions to upgrade. Admins can enter the iOS/iPadOS version to install and schedule the installation.

  These settings are configurable in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, go to [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

- **Software update deferral policies**

  These MDM policies hide updates for up to 90 days. They prevent users from manually updating their device to a version that hasn't been approved. This feature doesn't control when the updates are applied.

  These settings are configurable in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information, go to [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md).

With these features, admins can make sure their Apple devices are running a specific software version and can control the release of updates across their devices.

### ✅ Create policies that support many time zones

All policy times use Coordinated Universal Time (UTC). The device's local timezone isn't used.

To minimize the number of policies you have to create and manage, create a configuration that supports many time zones. Don't create a separate policy for each time zone.

For example, in the United States, there are four primary time zones: Pacific (UTC-8), Mountain (UTC-7), Central (UTC-6) and Eastern (UTC-5). You can create separate policies for each time zone. Or, create one or two policies that achieve the same result.

### ✅ Be careful with version settings

When you create software update policies, be aware of the broader impact of the version details in all your policies.

For example:

- You configure a policy that delays updates for 90 days. If there's an enrollment restriction policy that requires devices have a recent iOS/iPadOS version, then after a device reset, devices could be blocked from enrolling.

- You create a compliance policy that requires a minimum iOS/iPadOS version that's recent. With this policy, devices on older releases become noncompliant. If you use Conditional Access to enforce compliance, then users are blocked and can't work.

## Common industry scenarios

Apple devices are used in various industries, including enterprise, retail, manufacturing, and education. Most device use cases can be categorized into the following types:

- **1:1**: Devices are used by only one person.
- **Shared**: Devices are used by more than one person.
- **Dedicated**: Devices are used for a specific business purpose, like a kiosk or digital signage.

The following table includes common industry terminology that this article uses:

| Industry | Terminology | Use case |
| --- | --- | --- |
| Enterprise | Knowledge worker | 1:1 |
| Retail | Kiosk  | Dedicated |
| Manufacturing | Factory machine | Mission critical |
| Education | Assigned device | Shared |

This section describes some common industry scenarios and gives examples of Intune policies.

### Knowledge workers

This group is people with gained knowledge that work in enterprise businesses and organizations. Their knowledge and thinking ability are their job. Some examples include engineers, content developers, programmers, accountants, communications, consultants, and so on.

Knowledge workers typically have their own device that's only used by them. It's not shared with other users or other knowledge workers.

In scenarios like knowledge worker devices, the primary goal is for the update process to be as simple and quick as possible. Their apps are mostly store-based, and the apps should remain compatible with the latest OS version. On these devices, users are typically tolerant of prompts for updates and/or choosing a convenient time for reboots.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Basic update configuration
> * The latest most up-to-date version
> * Automatic updates

**Scenario example**:

You're configuring an update profile for the knowledge workers at Contoso. These users mostly use Microsoft 365 apps and several Volume Purchase Program (VPP) apps.

As an admin, you're comfortable with:

- These devices running the latest released iOS/iPadOS version
- Downloading and installing updates as soon as the devices check-in with Intune
- Allowing end-users to decide when they install updates and reboot their devices to apply the updates

To accomplish these goals, you can use a policy with the following default settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/knowledge-worker-policy-settings.png" alt-text="Screenshot that shows the select version to install and schedule type software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Kiosks

These devices are typically in-store retail devices, and can be a desktop computer or a mobile device. They're used by employees to serve customers and used directly by customers for self-service tasks. They can also be a visual display that all customers see when they're on-premises.

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

You're configuring an iOS/iPadOS update profile for the kiosk devices at Contoso. These devices operate in a retail outlet. Your staff uses the devices to serve customers 7 days a week, including extended retail hours. The devices run a single Line of Business (LOB) kiosk app, which was developed in-house by Contoso. This internal application is only tested and validated on a quarterly basis.

You want to deploy the specific iOS/iPadOS version that this LOB app was recently tested with, which is iOS 16.3. If this kiosk application doesn't work correctly, then the retail outlet can't serve customers. The devices are connected to Wi-Fi and charge overnight when the retail outlet is closed to customers.

You chose an overnight servicing window of 10 hours where updates can be downloaded and applied, before the store opens.

To accomplish this task, create a policy with the following settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/kiosks-policy-settings.png" alt-text="Screenshot that shows the specific version to install and installing the updates on Monday nights for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Factory machines

These devices are often single purpose devices. They're used in mission critical areas, like manufacturing lines or specialized equipment control & monitoring. For example, it could be an Android tablet running control or monitoring software for a device that welds components.

In factory machine scenarios, the primary goal is to make sure devices behave in a consistent manner. Updates might need to be delayed so all application compatibility testing can complete. Installation and reboots occur at specific times and are typically deployed in a phased approach.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Advanced policy configuration
> * Strict version control
> * Slow release cycles

**Scenario example**:

You're configuring an update profile for devices on the manufacturing floor at Contoso's industrial facility. The facility runs 24x7, 365 days a year, except for a few hours of mandatory stoppage for safety inspections. These inspections happen early Sunday morning every week.

These devices run two vendor apps. To remain in a supported configuration, both apps are updated infrequently, and must run a specific version of the app and OS.

You want to deploy a specific, older iOS/iPadOS version (15) to these devices, as the app vendor doesn't support later releases yet. Since the devices are nearly always in use, you only have a small maintenance window once a week on Sunday.

You want to schedule updates during a two hour downtime window overnight on a Sunday.

To accomplish this task, create a policy with the following settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/factory-machines-policy-settings.png" alt-text="Screenshot that shows the specific version to install and installing the updates on Sundays for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Shared devices

Shared devices are used by many users who typically sign in and out of the device, including education environments. These devices can be terminal/desktop computers, tablets, laptops, and smartphones. They're often used in offices, classrooms, and retail stores.

For more information on managing shared iOS/iPadOS devices, go to [Shared device solutions for iOS/iPadOS](../enrollment/device-enrollment-shared-ios.md).

For iOS/iPadOS shared devices, to apply updates, all users must be signed out. The users can be signed out or the device can be rebooted, which automatically signs out users.

An update strategy and priorities for these devices typically include:

> [!div class="checklist"]
>
> * Advanced policy configuration
> * Predictable version control
> * Controlled update behavior

**Scenario example**:

In the morning, UserA signs in to the device to check email before going out on the floor. An hour later, UserB uses the same device to run some LOB apps.

You need to configure an update for this shared device. These shared devices are used by general knowledge workers who are in the office from 8AM – 5PM, Monday through Friday. You want the devices on the latest iOS/iPadOS version that supports all the apps used on the shared devices.

To keep the policy as simple as possible, you want the updates to install outside typical working hours, plus one hour for reboots or other actions.

To accomplish this task, this scenario involves two policies:

- In the first policy, you want all users signed out or want to reboot the device after a set amount of time. You can create an Apple Business Manager enrollment profile to sign out any users who are idle for more than 15 minutes (900 seconds):

  :::image type="content" source="./media/software-updates-guide-ios-ipados/shared-devices-maximum-seconds-policy-settings.png" alt-text="Screenshot that shows how to enroll without user affinity and setting the inactivity value for iOS/iPadOS devices in the Microsoft Intune admin center.":::

- In the second policy, schedule the update using the following settings:

  :::image type="content" source="./media/software-updates-guide-ios-ipados/shared-devices-outside-scheduled-time-policy-settings.png" alt-text="Screenshot that shows installing the latest version and outside scheduled time software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

## Related articles

- [Manage iOS/iPadOS software update policies in Intune](software-updates-ios.md)
- [Software updates planning guide and scenarios for BYOD and personal devices](software-updates-guide-personal-byod.md)
- [Software updates planning guide for managed Android devices](software-updates-guide-android.md)
- [Software updates planning guide for managed macOS devices](software-updates-guide-macos.md)
