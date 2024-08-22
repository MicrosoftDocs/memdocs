---
# required metadata

title: Use the settings catalog to configure managed software updates 
description: Use Microsoft Intune to configure Apple's declarative device management (DDM) settings to install a specific update by an enforced deadline. This feature uses the settings catalog to configure managed software updates for supervised iOS/iPadOS and managed macOS devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 08/21/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-updates
---

# Managed software updates with the settings catalog

You can use the Intune [settings catalog](../configuration/settings-catalog.md) to configure managed software updates for iOS/iPadOS and macOS devices. With managed software updates in Intune, you can:

- Choose an update to install using its OS version or build version.
- Enforce a deadline for the device to automatically install an update.
- Specify a URL that users can visit to learn more about updates.

This feature applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

Apple's declarative device management (DDM) allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

> [!TIP]
> To learn more about declarative software updates from Apple, go to:
>
> - [Apple Platform Deployment](https://support.apple.com/guide/deployment/software-update-declarative-configuration-depca14ecd4d/web) (opens Apple's website)
> - [Apple's session on exploring advances in declarative device management](https://developer.apple.com/videos/play/wwdc2023/10041/) (opens Apple's website)
> - [The software update configuration in Apple's developer documentation](https://developer.apple.com/documentation/devicemanagement/softwareupdateenforcementspecific#discussion) (opens Apple's website)

## Managed software updates vs software update policies

On Apple devices in Intune, you can create software update policies or managed software update policies. Both policy types can manage the install of software updates on devices. However, there are some differences between the two policy types.

Use the following information to help you decide which policy type to use.

| Feature | Managed software update policy | Software update policy|
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
| iOS/iPadOS | ❌ | ✅ |
| macOS | ❌ | ✅ |
| &nbsp;|&nbsp; | &nbsp;|
| **Downgrade versions** | &nbsp; | &nbsp; |
| iOS/iPadOS | ❌ | ❌ |
| macOS | ❌ | ❌ |
| &nbsp;|&nbsp; | &nbsp;|
| **Intune admin center policy type** | &nbsp; | &nbsp; |
| iOS/iPadOS | [Settings catalog](../configuration/settings-catalog.md) |[Update policies for iOS/iPadOS](software-updates-ios.md) |
| macOS | [Settings catalog](../configuration/settings-catalog.md) | [Update policies for macOS](software-updates-macos.md) |
| &nbsp;|&nbsp; | &nbsp;|
| **Minimum supported version** | &nbsp; | &nbsp; |
| iOS/iPadOS | 17.0 and later | - iOS 10.3 (supervised)<br/>- iPadOS 13.0 (supervised) |
| macOS | 14.0 and later | macOS 12.0 |

### Precedence

Managed software updates have precedence over other policies that configure software updates. If you configure managed software updates and also have other software update policies assigned, then it's possible the other update policies have no effect.

**iOS/iPadOS precedence order**:

1. Managed software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
2. Update policies (**Devices** > **Update policies for iOS/iPadOS**)

**macOS precedence order**:

1. Managed software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
2. Update policies (**Devices** > **Update policies for macOS**)
3. Software updates (**Settings catalog** > **System Updates** > **Software Update**)

## Configure the managed software updates policy

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Enter the following properties and select **Create**:

    - **Platform**: Select **iOS/iPadOS** or **macOS**.
    - **Profile**: Select **Settings catalog**.

4. In the **Basics** tab, enter the following information, and select **Next**:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. In **Configuration settings**, select **Add settings** > expand **Declarative Device Management** > **Software Update**.

6. Choose **Select all these settings** and then close the settings picker.

    :::image type="content" source="./media/managed-software-updates-ios-macos/ddm-software-update-category.png" alt-text="Screenshot that shows the settings catalog software update settings for Apple devices in Microsoft Intune.":::

7. Configure the settings:

    - **Details URL**: Enter a web page URL that has more information on the update. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
    - **Target Build Version**: Enter the target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`.

      If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.

   - **Target Date Time**: Select or manually enter the date and the time that specifies when to force the installation of the software update.

     > [!NOTE]
     > In a future release, the **UTC** text is being removed from the **Target Date Time** setting in the settings catalog UI.
   
     The **Target Date Time** setting schedules the update using the local timezone of the device. For example, an admin configures an update to install at 2PM. The policy schedules the update to happen at 2PM in the local timezone of devices that receive the policy. 

     - If the user doesn't trigger the software update before this time, then a one-minute countdown prompt is shown to the user. When the countdown ends, the device force installs the update and forces a restart.
     - If the device is powered off when the deadline is met, when the device powers back on, there's a one hour grace period. When the grace period ends, the device force installs the update and forces a restart.

      > [!IMPORTANT]
      > If you create a policy using this setting before the January 2024 release, then this setting shows **Invalid Date** for the value. The updates are still scheduled correctly and use the values you originally configured, even though it shows **Invalid Date**.
      > 
      > To configure a new date and time, you can delete the **Invalid Date** values, and select a new date and time. Or, you can create a new policy. If you create a new policy, to help avoid future confusion, remove the values in the original policy.

    - **Target OS Version**: Select or manually enter the target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

8. Select **Next**.

9. In the **Scope tags** tab (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, go to [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

10. Select **Next**.

11. In the **Assignments** tab, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](../configuration/device-profile-assign.md).

    > [!IMPORTANT]
    > Assignment filters are not supported for DDM-based policies.

12. Select **Next**.

13. In the **Review + create** tab, review the settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Monitoring managed software updates

Managed software updates use the same reporting as device configuration policies. For more information, go to [Monitor device configuration policies](../configuration/device-profile-monitor.md).

> [!IMPORTANT]
> A policy that reports Success only means that the configuration successfully installed on the device. Monitor the OS version of targeted devices to ensure that they update. After devices have updated to a later OS version than configured in the policy, the policy will report error as the device sees this as an attempt to downgrade. It's recommended to remove the older OS version policy from devices in this state.

## Delay visibility of updates

When you configure managed software updates, you might want to hide updates from users for a specified time period. To hide the updates, use a settings catalog policy that configures an update restriction.

A restriction period gives you time to test an update before it's available to users. After the restriction period ends, users can see the update. If your update policies don't install it first, then users can choose to install the update.

To create a restrictions policy, go to the **Settings catalog** > **Restrictions**. Some settings you can use to defer an update include:

- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay (macOS)
- Enforced Software Update Minor OS Deferred Install Delay (macOS)
- Enforced Software Update Non OS Deferred Install Delay (macOS)

:::image type="content" source="./media/managed-software-updates-ios-macos/settings-catalog-restrictions-delay-updates.png" alt-text="Screenshot that shows the settings catalog restrictions policy settings to delay or defer software updates in Microsoft Intune.":::

## Related articles

- [iOS/iPadOS software update policies in Intune](software-updates-ios.md)
- [macOS software update policies in Intune](software-updates-macos.md)
- [Software updates planning guide for supervised iOS/iPadOS devices in Intune](software-updates-guide-ios-ipados.md)
- [Software updates planning guide for managed macOS devices in Intune](software-updates-guide-macos.md)
