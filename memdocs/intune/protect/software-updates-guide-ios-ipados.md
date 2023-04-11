---
title: Admin checklist for iOS/iPadOS software updates in Microsoft Intune
description: 
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/11/2023
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: ahamil, brenduns
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# iOS/iPadOS software updates admin checklist and scenarios in Microsoft Intune

Keeping your mobile devices up to date is critical. You need to reduce risk of security events and ensure minimal disruption to the business and users. For supervised devices, Intune can manage the updates that are available to a device, when the device is updated, and provide reporting on the update status.

## Admin checklist

This section lists the Microsoft-recommended strategies to install software updates on your iOS/iPadOS devices.

### ✔️ Manage updates with policies

It's recommened you create policies that update your devices. It's not recommended to put this responsbility on end users.

By default, users receive notifications and/or see the latest updates available on their devices (Settings > General > Software Updates). Users can choose to download and install updates whenever they want.

When users install their own updates (instead of admins managing the updates), it can disrupt user productivity and business tasks. For example:

- Users can start an update when they want, and might not be able to work while an update is installing.

- Users can apply updates that your organization hasn't approved. This decision can cause issues with application compatibility, changes to the operating system, or changes to the user experience that disrupt device use.

- Users can avoid applying required updates that impact security or app compatibility. This situation can leave the devices at risk and/or prevent the devices from functioning.

### ✔️ Keep automatic updates enabled

Starting with iOS/iPadOS 12, when updates are available, Apple devices automatically install the updates. By default, this feature is enabled on new devices.

To use use this automatic patching and install updates faster, make sure the devices are:

- Powered on
- Plugged in
- Connected to the Internet  

When the devices are powered on, plugged in, and connected to the Internet, then the updates automatically download & install, and the device reboots. If the device doesn't meet these conditions, then the updates won't automatically download and install.

To keep your devices on the most current version and with minimal effort from you, keep the Automatic updates feature enabled:

:::image type="content" source="./media/software-updates-guide-ios-ipados/apple-automatic-update-settings.png" alt-text="Screenshot that shows automatic update settings on iOS/iPadOS Apple devices.":::

If automatic updates are disabled, then:

- Admins can't change these settings with policies.
- Users need to manually change these settings on their devices.
- If users can't change these settings, then you must reset and reprovision the device. ??Why? This seems extreme? Remote actions?

Automatic updates work with other update policies, which provides a good experience for admins and end users.

You can also force users to update their devices:

- Use [Enrollment Restrictions](../enrollment/create-device-platform-restrictions.md) to prevent users from enrolling devices that aren't current.
- Create [compliance policies](../protect/compliance-policy-create-ios.md) to determine the devices that aren't updated.
- Create [Conditional Access (CA) policies](../protect/create-conditional-access-intune.md) to block devices that aren't updated. The CA policies can also prompt users to install current updates so they regain access.

?? What about iOS/iPadOS 11 and older??

### ✔️ Use the built-in settings

To manage updates, Apple has the following options:

- **Software update policies**

  These policies offer a controlled roll-out of a specific version. You can also force devices on older versions to upgrade. Admins can specify the iOS/iPadOS version to install and schedule the installation.

- **Software update deferral policies**

  These policies hide updates for up to 90 days. This feature doesn't control when the updates are applied. It can help prevent users from manually updating their device to a version that hasn't been approved.

With these features, admins can make sure their Apple devices are running a specific software version and can control the release of updates across their devices.

These settings are configurable in the Microsoft Intune admin center. For more information, go to [Manage iOS/iPadOS software update policies in Intune](../protect/software-updates-ios.md).

### ✔️ Create policies that support many time zones

All policy times use Coordinated Universal Time (UTC). The device's local timezone isn't used.

Create a configuration that supports many time zones, rather than creating a separate policy for each time zone. The idea is to minimize the number of policies you have to create and manage.

For example, in the United States, there are four primary time zones: Pacific (UTC-8), Mountain (UTC-7), Central (UTC-6) and Eastern (UTC-5). You can create separate policies for each time zone. Or, create one or two policies that achieve the same result.

### ✔️ Be careful with version settings

When you create software update policies, be aware of the broader impact of the version details in all your policies.

For example, you configure a policy that delays updates for 90 days. If there's an enrollment restriction policy that requires devices have a recent iOS/iPadOS version, then after a device reset, devices could be blocked from enrolling.

In another example, you create a compliance policy that requires a minimum iOS/iPadOS version that's recent. With this policy, devices on older releases become non-compliant. If you use conditional access to enforce compliance, then user are blocked and can't work.

## Common industry scenarios

Apple devices are used in a variety of industries, including enterprise, retail, manufacturing, and education. Most device use cases can be categorized into the following types:

- **1:1**: Devices are used by only one person.
- **Shared**: Devices are used by more than one person.  
- **Dedicated**: Devices are used for a specific business purpose, like a kiosk or digital signage.

This section describes some common industry scenarios and gives examples of Intune policies.

??Not sure the following table is needed??

This table can help map your industry specific terminology to use cases presented in this section:

| Industry | Terminology | Use case |
| --- | --- | --- |
| Enterprise | Knowledge worker | 1:1 |
| Retail | Kiosk  | Dedicated |
| Manufacturing | Factory machine | Mission critical |
| Education | Assigned Device | Shared |

### Knowledge workers

This group are people with gained knowledge. This knowledge and their thinking ability is their job. Some examples include engineers, content developers, programmers, accountants, communications, consultants, and so on.

Knowledge workers typically have their own device that's only used by them. It's not shared with other users or other knowledge workers.

In scenarios like knowledge worker devices, the primary goal is for the update process be as simple and quick as possible. Their apps are mostly store-based, and the apps should remain compatible with the latest OS version. On these devices, users are typically tolerant of prompts for updates and/or choosing a convenient time for reboots.

When creating an update strategy for these devices, the priorities typically include:

✔️ Simple update configuration  
✔️ The latest most up-to-date version  
✔️ Automatic updates

**Scenario example**:

You're configuring an update profile for the knowledge workers at Contoso. These users mostly use Microsoft 365 apps and several Volume Purchase Program (VPP) apps.

As an admin, you're comfortable with:

- These devices running the latest released iOS/iPadOS version
- Downloading and installing updates as soon as the devices check-in with Intune
- Allowing end-users to decide when they install updates and reboot their devices to apply the updates

To accomplish these goals, you can use a simple policy with the following default settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/knowledge-worker-policy-settings.png" alt-text="Screenshot that shows the select version to install and schedule type software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Kiosks

In Kiosk like scenarios the primary goal is to ensure that the device is up to date with approved OS updates, that updates versions are managed by the administrator, and that installation and reboot occur at a time that is not during business hours.

When creating an update strategy for these devices, the priorities typically include:

✔️ Simple update configuration  
✔️ Predictable version control  
✔️ Predictable release cycles

**Scenario example**:

You're configuring an iOS update profile for the kiosk devices at Contoso. These devices operate in a retail outlet. Your staff use the devices to serve customers 7 days a week during extended retail hours. The devices run a single Line of Business (LOB) kiosk app, which was developed by Contoso. This internal application is only tested and validated on a quarterly basis.

You want to deploy the specific version of iOS/iPadOS that this app was recently tested with, which is iOS 16.3. If this kiosk application does not work correctly, the retail outlet can't serve customers. The devices are left connected to wi-fi and charging overnight while the retail outlet is closed to customers. So, you chose an overnight servicing window of 10 hours where updates can be downloaded and applied, before the store opens for trading each morning.

To accomplish this task, create a policy with the following settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/kiosks-policy-settings.png" alt-text="Screenshot that shows the select version to install and scheduled time window software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Factory machines

??Need some text on what factory machines are, and examples.??

In Factory Machine scenarios, the primary goal is to make sure devices behave in a consistent manner. Updates may need to be delayed so all application compatibility testing has been completed. Installation and reboots occur at specific times and are typically deployed in a phased approach.

When creating an update strategy for these devices, the priorities typically include:

✔️ Advanced policy configuration  
✔️ Strict version control  
✔️ Slow release cycles

**Scenario example**:

You're configuring an update profile for devices on the manufacturing floor at Contoso's industrial facility. The facility runs 24x7, 365 days a year, except for a few hours of mandatory stoppage for safety inspections. These inspections happen early Sunday mornings each week.

These devices run two vendor apps. To remain in a supported configuration, both apps are updated infrequently, and must run a specific version of the app, operating system, etc.

You want to deploy a specific, older iOS/iPadOS version (15) to these devices, as the app vendor doesn't support later releases yet. Since the devices are nearly always in use, you only have a small maintenance window once a week on Sunday. So, you want to schedule updates during a 2-hour downtime window overnight on a Sunday.

To accomplish this task, create a policy with the following settings:

:::image type="content" source="./media/software-updates-guide-ios-ipados/factory-machines-policy-settings.png" alt-text="Screenshot that shows the select version to install and scheduled time window software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

### Shared devices

Shared devices are used by many users who typically sign in and out of the device. These devices can be terminal/desktop computers, tablets, laptops, and smartphones. They're often used in offices, classrooms, and retail stores.

For iOS/iPadOS shared devices, to apply updates, all users must be signed out. The users can be signed out or the device can be rebooted, which automatically signs out users.

When creating an update strategy for these devices, the priorities typically include:

✔️ Advanced policy configuration  
✔️ Predictable version control  
✔️ Controlled update behavior

**Scenario example**:

In the morning, UserA signs in to the device to check email before going out on the floor. An hour later, UserB uses the same device to run some LOB apps.

You need to configure an update for this shared device. These shared devices are used by general knowledge workers who are in the office from 8AM – 5PM, Monday through Friday. Your want the devices on the latest iOS/iPadOS version that supports all the apps used on the shared devices.

To keep the policy as simple as possible, you want the updates to install outside typical working hours, plus one hour for reboots or other actions.

To accomplish this task, this scenario involves two policies:

- In the first policy, you schedule the update using the following settings:

  :::image type="content" source="./media/software-updates-guide-ios-ipados/shared-devices-outside-scheduled-time-policy-settings.png" alt-text="Screenshot that shows installing the latest version and outside scheduled time software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

- You want all users signed out or reboot the device. In the second policy, you can create an Apple Business Manager enrollment profile to sign out any users who are idle for more than 15 minutes (900 seconds):

  :::image type="content" source="./media/software-updates-guide-ios-ipados/shared-devices-maximum-seconds-policy-settings.png" alt-text="Screenshot that shows installing the latest version and outside scheduled time software update settings for iOS/iPadOS devices in the Microsoft Intune admin center.":::

## Next steps
