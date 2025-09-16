---
# required metadata

title: Use the settings catalog to configure DDM software updates 
description: Use Microsoft Intune to configure Apple's declarative device management (DDM) settings to install a specific update by an enforced deadline. This feature uses the settings catalog to configure managed software updates for supervised iOS/iPadOS and managed macOS devices.
keywords:
author: paolomatarazzo
ms.author: paoloma
manager: laurawi
ms.date: 08/18/2025
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

# DDM software updates with the settings catalog in Microsoft Intune

You can use the Intune [settings catalog](../configuration/settings-catalog.md) to configure managed software updates for iOS/iPadOS and macOS devices. Managed software updates uses Apple's declarative device management (DDM).

With DDM managed software updates in Intune, you can:

- Choose an update to install using its OS version or build version.
- Enforce a deadline for the device to automatically install an update.
- Specify a URL that users can visit to learn more about updates.

This feature applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

Apple's declarative device management (DDM) allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

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
| iOS/iPadOS | [Settings catalog](../configuration/settings-catalog.md) |[Update policies for iOS/iPadOS](software-updates-ios.md) |
| macOS | [Settings catalog](../configuration/settings-catalog.md) | [Update policies for macOS](software-updates-macos.md) |
| &nbsp;|&nbsp; | &nbsp;|
| **Minimum supported version** | &nbsp; | &nbsp; |
| iOS/iPadOS | 17.0 and later | - iOS 10.3 (supervised)<br/>- iPadOS 13.0 (supervised) |
| macOS | 14.0 and later | macOS 12.0 |

### Precedence

DDM software updates have precedence over other policies that configure software updates. If you configure DDM software updates and also have other MDM software update policies assigned, then it's possible the other update policies have no effect.

**iOS/iPadOS precedence order**:

1. DDM software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
2. MDM update policies (**Devices** > **Update policies for iOS/iPadOS**)

**macOS precedence order**:

1. DDM software updates (**Settings catalog** > **Declarative Device Management** > **Software Update**)
2. MDM update policies (**Devices** > **Update policies for macOS**)
3. MDM software updates (**Settings catalog** > **System Updates** > **Software Update**)

## Configure the automatic DDM software updates policy

You can use the settings catalog to configure a policy that automatically enforces the latest update available for devices, so you don't have to manually update the target OS version and target date time settings each time that Apple releases a new update.

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Enter the following properties and select **Create**:

    - **Platform**: Select **iOS/iPadOS** or **macOS**.
    - **Profile**: Select **Settings catalog**.

4. In the **Basics** tab, enter the following information, and select **Next**:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. In **Configuration settings**, select **Add settings** > expand **Declarative Device Management** > **Software Update Enforce Latest**.

6. Choose **Select all these settings** and then close the settings picker.

    :::image type="content" source="./media/managed-software-updates-ios-macos/ddm-software-updates-enforce-latest.png" alt-text="Screenshot that shows the settings catalog software update enforce latest settings for Apple devices in Microsoft Intune." lightbox="./media/managed-software-updates-ios-macos/ddm-software-updates-enforce-latest.png":::

7. Configure the settings:

    - **Delay in Days**: Specify the number of days that should pass before a deadline is enforced. This delay is based on either the posting date of the new update when released by Apple, or when the policy is configured.
    - **Install Time**: Specify the local device time for when updates are enforced.

      > [!IMPORTANT]
      > The Install Time setting is configured using the 24-hour clock format where midnight is 00:00 and 11:59pm is 23:59. Ensure that you include the leading 0 on single digit hours. For example, 01:00, 02:00, 03:00.

8. Select **Next**.

9. In the **Scope tags** tab (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, go to [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

10. Select **Next**.

11. In the **Assignments** tab, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](../configuration/device-profile-assign.md).

    > [!IMPORTANT]
    > Assignment filters are not supported for DDM-based policies.

12. Select **Next**.

1. In the **Review + create** tab, review the settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

> [!NOTE]
> The `retrieveDeviceConfigurationAvailableOptions` function of the [deviceManagementConfigurationSettingDefinition resource type](/graph/api/resources/intune-deviceconfigv2-devicemanagementconfigurationsettingdefinition?view=graph-rest-beta) requires delegated user authentication. Application permissions cannot be used for this endpoint. 

## Configure the manual DDM software updates policy

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

    :::image type="content" source="./media/managed-software-updates-ios-macos/ddm-software-update-category.png" alt-text="Screenshot that shows the settings catalog software update settings for Apple devices in Microsoft Intune." lightbox="./media/managed-software-updates-ios-macos/ddm-software-update-category.png":::

7. Configure the settings:

    - **Details URL**: Enter a web page URL that has more information on the update. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
    - **Target Build Version**: Enter the target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`.

      If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.

   - **Target Date Time**: Select or manually enter the date and the time that specifies when to force the installation of the software update.
   
     The **Target Date Time** setting schedules the update using the local timezone of the device. For example, an admin configures an update to install at 2PM. The policy schedules the update to happen at 2PM in the local timezone of devices that receive the policy.

     - If the user doesn't trigger the software update before this time, then a one-minute countdown prompt is shown to the user. When the countdown ends, the device force installs the update and forces a restart.
     - If the device is powered off when the deadline is met, when the device powers back on, there's a one hour grace period. When the grace period ends, the device force installs the update and forces a restart.

    - **Target OS Version**: Select or manually enter the target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

8. Select **Next**.

9. In the **Scope tags** tab (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, go to [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

10. Select **Next**.

11. In the **Assignments** tab, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](../configuration/device-profile-assign.md).

    > [!IMPORTANT]
    > Assignment filters are not supported for DDM-based policies.

12. Select **Next**.

13. In the **Review + create** tab, review the settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Monitoring DDM software updates

To monitor software updates for Apple devices, you can use the following methods:

- DDM software updates use the same reporting as device configuration policies. For more information, see [Monitor device configuration policies](../configuration/device-profile-monitor.md).

  > [!IMPORTANT]
  > A policy that reports Success only means that the configuration policy successfully installed on the device. Monitor the OS version of targeted devices to ensure that they update. After devices have updated to a later OS version than configured in the policy, the policy reports an error as the device sees this task as an attempt to downgrade. It's recommended to remove the older OS version policy from devices in this state.  

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

:::image type="content" source="./media/managed-software-updates-ios-macos/settings-catalog-restrictions-delay-updates.png" alt-text="Screenshot that shows the settings catalog restrictions policy settings to delay or defer software updates in Microsoft Intune." lightbox="./media/managed-software-updates-ios-macos/settings-catalog-restrictions-delay-updates.png":::

## Related articles

- [iOS/iPadOS software update policies in Intune](software-updates-ios.md)
- [macOS software update policies in Intune](software-updates-macos.md)
- [Software updates planning guide for supervised iOS/iPadOS devices in Intune](software-updates-guide-ios-ipados.md)
- [Software updates planning guide for managed macOS devices in Intune](software-updates-guide-macos.md)
- [Declarative Apple software update reports in Intune](software-updates-reports-apple-declarative-based.md)
