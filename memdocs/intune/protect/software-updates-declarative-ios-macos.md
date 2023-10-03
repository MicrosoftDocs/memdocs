---
# required metadata

title: Use the settings catalog to configure declarative software updates 
description: Use Microsoft Intune to configure Apple's declarative device management (DDM) settings to install a specific update by an enforced deadline. This feature uses the settings catalog to configure declarative software updates for supervised iOS/iPadOS and managed macOS devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 10/23/2023
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
---

# Manage declarative software updates with the settings catalog

You can use the Intune [settings catalog](../configuration/settings-catalog.md) to configure declarative software updates for supervised iOS/iPadOS and macOS devices. With declarative software updates in Intune, you can:

- Choose an update to install using its OS version or build version.
- Enforce a deadline for the device to automatically install an update.
- Specify a URL that users can visit to learn more about updates.

This feature applies to:

- iOS/iPadOS 17.0 and later (supervised)
- macOS 14.0 and later

Apple's declarative device management (DDM) allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

> [!TIP]
> To learn more about declarative software updates from Apple, go to:
>
> - [Apple's session on exploring advances in declarative device management](https://developer.apple.com/videos/play/wwdc2023/10041/) (opens Apple's website)
> - [The software update configuration in Apple's developer documentation](https://developer.apple.com/documentation/devicemanagement/softwareupdateenforcementspecific#discussion) (opens Apple's website)

## Declarative software updates vs software update policies

Declarative software updates take precedence over iOS/iPadOS and macOS software update policies.

Can the two policy types work together? Or, is this a conflict scenario?

## Configure the DDM software updates policy

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS** or **macOS**.
    - **Profile**: Select **Settings catalog**.

    Select **Create**.

4. In **Basics**, enter the following information:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

    Select **Next**.

5. In **Configuration settings**, select **Add settings** > Expand **Declarative Device Management** > **Software Update**.

    Configure the following settings:

    - **Details URL**: Enter a web page URL that has more information on the update. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
    - **Target Build Version**: Enter the target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`.

      If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.

    - **Target Local Date Time**: Enter the local date time value that specifies when to force install the software update. If the user doesn't trigger the software update before this time, then the device force installs it.

      After the deadline passes, there's a one hour grace period. Then, the device forces a restart.

    - **Target OS Version**: Enter the target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

6. Select **Next**.
7. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, go [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

8. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](../configuration/device-profile-assign.md).

    Select **Next**.

9. In **Review + create**, review the settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Delay visibility and configure experience of updates

When you configure declarative software updates, you might want to hide updates from users for a specified time period. To hide the updates, use a settings catalog policy that configures an update restriction.

A restriction period gives you time to test an update before it's available to users. After the restriction period ends, users can see the update. If your update policies don't install it first, then users can choose to install the update.

To create a restrictions policy, go to the **Settings catalog** > **Restrictions**. Some settings you can use to defer an update include:

- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay (macOS)
- Enforced Software Update Minor OS Deferred Install Delay (macOS)
- Enforced Software Update Non OS Deferred Install Delay (macOS)

:::image type="content" source="./media/software-updates-declarative-ios-macos/settings-catalog-restrictions-delay-updates.png" alt-text="Screenshot that shows the settings catalog restrictions policy settings to delay or defer software updates in Microsoft Intune.":::

In the **Settings catalog**, you can also use the **System Updates** > **Software Update** settings to manage how users manually interact with updates through their macOS system. However, updates from a targeted update policy override these settings.

## Related articles

- [iOS/iPadOS software update policies in Intune](software-updates-ios.md)
- [macOS software update policies in Intune](software-updates-macos.md)
- [Software updates planning guide for supervised iOS/iPadOS devices in Intune](software-updates-guide-ios-ipados.md)
- [Software updates planning guide for managed macOS devices in Intune](software-updates-guide-macos.md)
