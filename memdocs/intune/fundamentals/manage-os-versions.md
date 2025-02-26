---
# required metadata

title: Manage device operating system versions with Intune
titleSuffix: Microsoft Intune
description: Learn about the methods for managing device operating system versions supported by Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/24/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 361ef17b-1ee0-4879-b7b1-d678b0787f5a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
- intune-scenario
---

# Manage operating system versions with Microsoft Intune

On modern mobile and desktop platforms, major updates, patches, and new versions release at a rapid pace. You have controls to fully manage updates and patches on Windows, but other platforms like iOS/iPadOS and Android require your end users to participate in the process. Microsoft Intune has the capabilities to help you structure your operating system version management across different platforms.

Intune can help you address these common scenarios:

- Determine which operating system versions are on your end-user devices
- Control access to organizational data on devices while you validate a new operating system release
- Encourage/require end users to upgrade to the latest operating system version approved by your organization
- Manage an organization-wide rollout to a new operating system version
  
## Operating system version control using Intune mobile device management enrollment restrictions

With [device enrollment restrictions](../enrollment/enrollment-restrictions-set.md), you can restrict devices from enrolling in Intune based on certain device attributes. The goal is to allow users to enroll only devices that are compliant to your organizations expectations, and prevent enrollment of devices that aren't compliant where they could gain access to your organizations resources. You can create *enrollment device platform restriction* policies for the following platforms:

- Android
- iOS/iPadOS
- macOS
- Windows

The device platform restriction policies for each platform type include both a minimum and maximum allowed operating system versions, as seen in the following screen capture of an iOS policy:

:::image type="content" source="./media/manage-os-versions/os-version-platform-configuration.png" alt-text="Platform configuration restrictions page.":::

### In practice

Organizations use device type restrictions to control access to organizational resources by using the following settings:

1. Use minimum operating system version to ensure can only enroll current and supported platforms in your organization.
2. Leave maximum operating system unspecified (no limit) or set it to the last version your organization has validated for use, to allow time for internal testing of new operating system releases.

For more information, see [Create a device platform restriction](../enrollment/create-device-platform-restrictions.md).

## Operating system version reporting and compliance with Intune device compliance policies

Intune device compliance policies provide you with the following tools:

- Specify compliance rules that define required configurations for devices.
- View compliance reports to understand which devices are noncompliant, and to which settings in your policies.
- Act on noncompliance results via device quarantine and Conditional Access policies that prevent noncompliant devices from accessing your organizations resources.

Like enrollment restrictions, device compliance policies include both minimum and maximum operating system versions. Policies also have a compliance timeline to provide your users a grace period to get compliant. Device compliance policies keep your enrolled end-user devices compliant with your organizations expectations.

:::image type="content" source="./media/manage-os-versions/os-version-actions-noncompliance.png" alt-text="Device compliance - actions for noncompliant devices":::

### In practice

Organizations are using device compliance policies for the same scenarios as enrollment restrictions. These policies keep users on current, validated operating system versions in your organization. When end-user devices fall out of compliance, access to organizational resources can be blocked via Conditional Access until end users are within the supported operating system range for your organization. End users are notified that they're out of compliance and they're provided the steps to regain access.

For more information, see [Get started with device compliance](../protect/device-compliance-get-started.md).

## Operating system version controls using Intune app protection policies

Intune app protection policies and mobile application management (MAM) access settings let you specify the minimum operating system version at the app layer. This lets you inform and encourage, or require, your end users to update their operating system to a specified minimum version.

You have two options:

- **Warn** - Warn informs the end user that they should upgrade if they open an app with an application protection policy or MAM access settings on a device with an operating system version below the specified version. Access is allowed for the app and organizational data.

  ![Image of the Android update warning dialog](./media/manage-os-versions/os-version-update-warning.png)

- **Block** - Block informs the end user that they must upgrade when they open an app with an application protection policy or MAM access settings on a device with an operating system version below the specified version. Access isn't allowed for app and organizational data.

  ![Image of the App access blocked dialog](./media/manage-os-versions/os-version-access-blocked.png)

### In practice

Organizations are using app protection policy settings today when apps are opened or resumed as a way to educate end users about the need to keep their apps current. An example configuration is that end users are warned on current version minus one and blocked on current version minus two.

For more information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

## Managing multiple OS versions using Intune app protection policies

In App Protection Policies (APP), you can only configure one minimum OS version in the conditional
launch settings but you could create multiple APPs with different
minimum OS values. However, because APPs are assigned to user groups,
this means a user with multiple devices that are running different OS
versions could face conflicting OS requirements when accessing protected
resources.

To allow multiple APPs with different OS requirements to be targeted to
the same user, you can [create
filters](../fundamentals/filters.md)
which target the APP to a specific OS version.

There are two types of filters for Intune: Managed devices and Managed
apps. APP only supports Managed apps filters.

**Creating filters**

To use filters with APPs, you must create a filter for each specific OS
version you want to target:

1.  Navigate to the Microsoft Intune admin center.

2.  Select **Tenant
    administration** \> **Filters** \> **Create** \> **Managed apps**.


3.  On the **Basics** page, enter a name for the filter which makes it
    easily identifiable and select the platform you want to target, in
    this example, iOS/iPadOS.


4.  On the **Rules** page, create a filter for the major OS release you
    wish target, for example, Property=osVersion(OS version),
    Operator=StartsWith, Value=18.

   - Optional: You can use the **Preview** button to check the **device,
user, and app** which match the specified filter.

5.  On the **Review and create** page, save the filter by selecting
    **Create.**

Repeat these steps to create additional filters for each platform and
major OS version you want to target, such as iOS 16 and 17.

**Create and target APP with a filter**

1.  Navigate to the Microsoft Intune admin center.

2.  Select **Apps** \> **App protection policies** \> **Create
    policy** \> Choose the platform you want to target with the APP,
    such as iOS/iPadOS.

3.  On the **Basics** page, enter a name for the policy which makes it
    easily identifiable.

4.  Complete the **Apps**, **Data protection** and **Access
    requirements** pages with the
    [iOS](../apps/app-protection-policy-settings-ios.md),
    [Android](../apps/app-protection-policy-settings-android.md)
    or
    [Windows](../apps/app-protection-policy-settings-windows.md)
    app protection policy settings which meet the requirements for your
    organization. Within the **Device conditions** section on the
    **Conditional launch page** (or Health Checks page for Windows APP),
    configure the OS minor or patch release you wish to set as the
    minimum version. For example, Setting=Min OS version, Value=18.2.1,
    Action=Block access/Wipe data/Warn, as per the action required for
    your organization.

5.  On the **Assignments** page, use the previously created filter to
    scope the policy assignment to the correct major OS version.

6.  On the **Review and create** page, save the policy by selecting
    **Create.**

In the example shown, the filter will target devices running iOS 18
and the APP conditional launch settings will require 18.2.1, ensuring
that the APP does not apply to devices running on other major version
of iOS.

Create additional APPs for each OS version, for instance:

-   Second policy for iOS 16: **Conditional launch, Device conditions**,
    Min OS version=16.7.10, filter, OS version, StartsWith=16.

-   Third policy for iOS 17: **Conditional launch, Device conditions,**
    Min OS version=17.7.2, filter OS version, StartsWith=17.

### In practice

Organizations can create multiple APPs that require different minimum OS versions. By doing this, you can filter the assignment of these APPs to only apply to each major OS version. This ensures that each APP is compatible with the specific OS version it is assigned to, providing a tailored approach to app protection.

As OS vendors release new minor OS updates or patches, you can also update each APP with the new minimum OS version. This continuous updating process ensures that your organization remains secure by always using the latest OS versions. Keeping your apps and OS versions up-to-date helps protect against vulnerabilities and enhances overall security.


## Managing a new operating system version rollout

You can use the Intune capabilities described in this article to help you move your organizations devices to a new operating system version within the timeline you define. The following steps provide a sample deployment model to move your users from operating system v1 to operating system v2 in seven days.

1. Use [device enrollment restrictions](../enrollment/enrollment-restrictions-set.md) to require operating system v2 as the minimum version to enroll the device. This ensures new end-user devices are compliant at enrollment time.
2. Use Intune [app protection policies](../apps/app-protection-policy.md) to warn users when a protected app opens or resumes that the newer operating system v2 is required.
3. Use [device compliance policies](../protect/device-compliance-get-started.md) to require operating system v2 as the minimum version for a device to be compliant. Use **Actions for noncompliance** to allow a seven-day grace period and to send end users an email notification with your timeline and requirements.
   - These policies can inform end users that their devices need to be updated through email, the Intune Company Portal, and when the app is opened for apps enabled with an app protection policy.
   - You can run a compliance report to identify users that are out of compliance.
4. Use Intune app protection policies to block users when an app opens or resumes if the device isn't running operating system v2.
5. Use device compliance policies to require operating system v2 as the minimum version for a device to be compliant.
   - These policies require devices to be updated for them to continue to access organizational data. Protected services are blocked when used with device Conditional Access. Apps enabled with an app protection policy are blocked when opened or when they access organizational data.


## Next steps

Use the following resources to manage the operating system versions that are in use in your organization:

- [Set device type restrictions](../enrollment/enrollment-restrictions-set.md)
- [Get started with device compliance](../protect/device-compliance-get-started.md)
- [How to create and assign app protection policies](../apps/app-protection-policies.md)
