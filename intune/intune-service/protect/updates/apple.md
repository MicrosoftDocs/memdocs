---
title: Configure Software Updates For Apple devices
description: Use Microsoft Intune to configure Apple's declarative device management (DDM) settings for Software Updates.
author: paolomatarazzo
ms.author: paoloma
ms.date: 09/24/2025
ms.topic: how-to
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
- sub-updates
---

# Configure software updates for Apple devices

Keeping devices updated is essential for maintaining enterprise security, performance, and compliance. Updates often include critical patches, bug fixes, and feature enhancements. Without a consistent update strategy, organizations risk exposing endpoints to vulnerabilities and compatibility issues.

Microsoft Intune enables IT admins to configure and enforce update policies for Apple devices. You can schedule updates during maintenance windows, set enforcement deadlines, and reduce user disruption.

This article explains how to configure update policies in Intune using Apple's Declarative Device Management (DDM) model. DDM provides greater reliability and autonomy than older MDM-based update policies, which are now deprecated.

[!INCLUDE [platform-requirements](../../includes/h2/platform-requirements.md)]

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS 17.0 and later
> - macOS 14.0 and later

## Configuration

When designing your Apple device update strategy, align with your organization's security policies, user experience expectations, and compliance mandates. Intune supports two primary policy models for managing software updates:

- **Latest version policy**: automatically installs the latest eligible OS version after a defined deferral period. With this model:

  - You configure a deferral period (in days) and an installation time.
  - Updates are hidden from users during the deferral window and become visible once the period ends.  
  - Devices autonomously install the update within the declared deadline—no manual triggers required.

  This model is ideal for organizations that prioritize rapid patching, regulatory compliance, and minimal IT overhead.

- **Targeted version policy** - offers granular control over which OS version is installed and when. With this model:

  - You specify the required OS version and set a precise installation deadline.
  - A help URL can be provided for user assistance.
  - Devices enforce compliance independently, without manual enforcement.

  This model is best suited for environments with strict app compatibility requirements, phased deployment strategies, or formal change management workflows.

# [**Latest version**](#tab/automatic-updates)

1. [Create a settings catalog policy](/intune/intune-service/configuration/settings-catalog) for the iOS/iPadOS or macOS platform and use the following settings:

    | Category | Setting name and value |
    |--|--|--|
    | **Declarative Device Management** > **Software Update Enforce Latest** | **Delay in Days**<br><br> Specify the number of days that should pass before a deadline is enforced. This delay is based on either the posting date of the new update when released by Apple, or when the policy is configured.|
    | **Declarative Device Management** > **Software Update Enforce Latest** | **Install Time**<br><br> Specify the local device time for when updates are enforced. The Install Time setting is configured using the 24-hour clock format where midnight is `00:00` and 11:59pm is `23:59`. Ensure that you include the leading 0 on single digit hours. For example, `01:00`, `02:00`, `03:00`.|

1. [Assign the policy](/intune/intune-service/configuration/device-profile-assign) to a group to target users or devices.

    > [!IMPORTANT]
    > Assignment filters are not supported for DDM-based policies.

# [**Targeted version**](#tab/manual-updates)

1. [Create a settings catalog policy](/intune/intune-service/configuration/settings-catalog) for the iOS/iPadOS or macOS platform and use the following settings:

    | Category | Setting name and value |
    |--|--|--|
    | **Declarative Device Management** > **Software Update** | **Details URL**<br><br> Enter a web page URL that has more information on the update. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.|
    | **Declarative Device Management** > **Software Update** | **Target Build Version**<br><br> Enter the target build version to update the device to, like `25A354`. The build version can include a supplemental version identifier, like `25A354a`.<br><br>If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.|
    | **Declarative Device Management** > **Software Update** | **Target Date Time**<br> Select or manually enter the date and the time that specifies when to force the installation of the software update.<br><br>The **Target Date Time** setting schedules the update using the local timezone of the device. For example, an admin configures an update to install at 2PM. The policy schedules the update to happen at 2PM in the local timezone of devices that receive the policy.<br><br>If the user doesn't trigger the software update before this time, then a one-minute countdown prompt is shown to the user. When the countdown ends, the device force installs the update and forces a restart.<br>If the device is powered off when the deadline is met, when the device powers back on, there's a one hour grace period. When the grace period ends, the device force installs the update and forces a restart.|
    | **Declarative Device Management** > **Software Update** | **Target OS Version**<br><br> Select or manually enter the target OS version to update the device to. This value is the OS version number, like `26.0`. You can also include a supplemental version identifier, like `26.0.1`.|

1. [Assign the policy](/intune/intune-service/configuration/device-profile-assign) to a group to target users or devices.

    > [!IMPORTANT]
    > Assignment filters are not supported for DDM-based policies.

---

## Policy precedence

When both Declarative Device Management (DDM) and Mobile Device Management (MDM) update policies are configured, DDM settings take precedence. If a device receives both DDM and MDM update instructions, the DDM policy will override MDM behavior—potentially rendering MDM update policies ineffective.

**iOS/iPadOS precedence order**:

1. DDM software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
1. MDM update policies (**Devices** > **Update policies for iOS/iPadOS**)

**macOS precedence order**:

1. DDM software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
1. MDM update policies (**Devices** > **Update policies for macOS**)
1. MDM software updates (**Settings catalog** > **System Updates** > **Software Update**)

> [!TIP]
> Avoid configuring conflicting DDM and MDM policies. Doing so may lead to unexpected results or policy enforcement gaps.

## Using the Software Update Settings declarative configuration

When you configure DDM software updates, you might want to manage aspects of the software update process leading up to the enforcement of an update. Using this configuration, you can:

- Require that an admin or standard user can perform updates on the device
- Control how users can manually interact with software update settings like automatic download and install or the behavior of Rapid Security Responses
- Hide updates from users for a specified time period
- Suppress update notifications up to one hour before the enforcement deadline
- Control whether users are allowed to update to the latest major update, latest minor update, or are offered both.

Previously in MDM, these settings were spread across multiple payloads such as Restrictions, Managed Settings, and Software Update. As of August 2024, it's recommended to use the DDM-based Software Update Settings configuration to manage updates. To create a Software Update Settings policy, go to the Settings catalog > Declarative Device Management (DDM) > Software Update Settings. More information on these settings is available in the documentation section for the [Software Update Settings declarative configuration](/mem/intune-service/configuration/apple-settings-catalog-configurations).

## Delay visibility of updates using MDM

> [!NOTE]
> As of August 2024, it's recommended to use the DDM-based Software Update Settings configuration to manage update settings such as deferrals.

When you configure DDM software updates, you might want to hide updates from users for a specified time period. To hide the updates, use a settings catalog policy that configures an update restriction.

A restriction period gives you time to test an update before it's available to users. After the restriction period ends, users can see the update. If your update policies don't install it first, then users can choose to install the update.

To create a restrictions policy, go to the **Settings catalog** > **Restrictions**. Some settings you can use to defer an update include:

- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay (macOS)
- Enforced Software Update Minor OS Deferred Install Delay (macOS)
- Enforced Software Update Non OS Deferred Install Delay (macOS)

:::image type="content" source="images/settings-catalog-restrictions-delay-updates.png" alt-text="Screenshot that shows the settings catalog restrictions policy settings to delay or defer software updates in Microsoft Intune." lightbox="images/settings-catalog-restrictions-delay-updates.png":::

## Monitor software updates

To monitor software updates for Apple devices, use the following methods:

- DDM software updates use the same reporting as device configuration policies. For more information, see [Monitor device configuration policies](../../configuration/device-profile-monitor.md).

  > [!IMPORTANT]
  > A policy that reports Success only means that the configuration policy successfully installed on the device. Monitor the OS version of targeted devices to ensure that they update. After devices have updated to a later OS version than configured in the policy, the policy reports an error as the device sees this task as an attempt to downgrade. It's recommended to remove the older OS version policy from devices in this state.

## Related articles

- [Software updates planning guide for supervised iOS/iPadOS devices in Intune](software-updates-guide-ios-ipados.md)
- [Software updates planning guide for managed macOS devices in Intune](software-updates-guide-macos.md)
- [Declarative Apple software update reports in Intune](apple-reports.md)

<!--
## DDM software updates vs MDM software update policies

On Apple devices in Intune, you can create MDM-based software update policies or DDM-managed software update policies. Both policy types can manage the install of software updates on devices. However, there are some differences between the two policy types.

> [!NOTE]
> Apple deprecated MDM-based software update workloads. Microsoft recommends you use DDM to install updates instead. For more information on these changes, see [support tip for moving to declarative device management for Apple software updates](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-move-to-declarative-device-management-for-apple-software-updates/4432177).

Use the following information to help you decide which policy type to use.

| Feature | Managed software update policy (DDM) | Software update policy (MDM) |
| --- | --- | --- |
| **Configure a specific update to install** | &nbsp; | &nbsp; |
| iOS/iPadOS | ✅ | ✅ |
| macOS | ✅ | ❌ |
| &nbsp;|&nbsp; | &nbsp;|
| **Enforces an update deadline** | &nbsp; | &nbsp; |
| iOS/iPadOS | ✅ | ❌ |
| macOS | ✅ | ❌ |
| &nbsp;|&nbsp; | &nbsp;|
| **Enter a help URL** | &nbsp; | &nbsp; |
| iOS/iPadOS | ✅ | ❌ |
| macOS | ✅ | ❌ |
| &nbsp;|&nbsp; | &nbsp;|
| **Auto deploy latest update** | &nbsp; | &nbsp; |
| iOS/iPadOS | ✅ | ✅ |
| macOS | ✅ | ✅ |
| &nbsp;|&nbsp; | &nbsp;|
| **Downgrade versions** | &nbsp; | &nbsp; |
| iOS/iPadOS | ❌ | ❌ |
| macOS | ❌ | ❌ |
| &nbsp;|&nbsp; | &nbsp;|
| **Intune admin center policy type** | &nbsp; | &nbsp; |
| iOS/iPadOS | [Settings catalog](../../configuration/settings-catalog.md) |[Update policies for iOS/iPadOS](software-updates-ios.md) |
| macOS | [Settings catalog](../../configuration/settings-catalog.md) | [Update policies for macOS](software-updates-macos.md) |
| &nbsp;|&nbsp; | &nbsp;|
| **Minimum supported version** | &nbsp; | &nbsp; |
| iOS/iPadOS | 17.0 and later | - iOS 10.3 (supervised)<br/>- iPadOS 13.0 (supervised) |
| macOS | 14.0 and later | macOS 12.0 |

-->
