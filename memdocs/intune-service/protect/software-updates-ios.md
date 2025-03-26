---
# required metadata

title: Use Microsoft Intune to manage software updates for supervised iOS/iPadOS devices
description: Use Microsoft Intune to manage system updates for supervised iOS/iPadOS devices.
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

ms.reviewer: annovich
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

# Manage iOS/iPadOS software update policies in Intune

You can use Microsoft Intune device configuration profiles to manage software updates for iOS/iPad devices that are enrolled as *supervised devices*.

A [supervised device](../enrollment/device-enrollment-program-enroll-ios.md#what-is-supervised-mode) is a device that enrolls through one of Apple's [Automated Device Enrollment (ADE)](https://deploy.apple.com/) options. Devices enrolled through ADE support management control through a mobile device management solution like Intune. ADE options include Apple Business Manager or Apple School Manager.

This feature applies to:

- iOS 10.3 and later (supervised)
- iPadOS 13.0 and later (supervised)

> [!TIP]
> You can use the [Intune settings catalog](../configuration/settings-catalog.md) to manage declarative software updates. Declarative device management (DDM) provides an improved user experience as the device handles the entire software update lifecycle. For more information, go to [Manage software updates with the settings catalog](managed-software-updates-ios-macos.md).

With policies for iOS software updates, you can:

- Choose to deploy the *latest update* that's available, or choose to deploy an older update, based on the update version number.

  When deploying an older update, you must also deploy a device restrictions profile to [restrict visibility of software updates](#delay-visibility-of-software-updates). Update profiles don't prevent users from updating the OS manually. Users can be prevented from updating the OS manually with a device configuration policy that restricts visibility of software updates.

- Specify a schedule that determines when the update installs. Schedules can be as simple as installing updates the next time that the device checks in. Or, creating date and time ranges during which updates can install or are blocked from installing.

  By default, devices check in with Intune about every eight hours. If an update is available through an update policy, the device downloads the update. The device then installs the update upon next check-in within your schedule configuration.

> [!NOTE]
>
> - iOS/iPadOS software updates that you send to a [Shared iPad](../enrollment/device-enrollment-shared-ipad.md) will install only when the device is charging and while no users are signed in to a *Shared iPad session* on the device. The iPad must be signed out of all user accounts and plugged into a power source for the device to update successfully.
>
> - If using [Autonomous Single App Mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam), the impact of OS updates should be considered as the resulting behavior may be undesirable. Consider testing to assess the impact of OS updates on the app you are running in ASAM. You can use Intune [*device restriction profiles*](../configuration/device-restrictions-ios.md#general) to configure ASAM.

> [!TIP]
> If you're new to configuring software updates or want some guidance based on common scenarios, go to:
>
> - [Software updates planning guide for supervised iOS/iPadOS devices](software-updates-guide-ios-ipados.md)
> - [Software updates planning guide for BYOD and personal devices](software-updates-guide-personal-byod.md)

## Configure the update policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Update policies for iOS/iPadOS** > **Create profile**.
3. On the **Basics** tab, specify a name for this policy, specify a description (optional), and then select **Next**.
4. On the **Update policy settings** tab, configure the following options:

   :::image type="content" source="./media/software-updates-ios/basics-tab.png" alt-text="Screenshot that shows sample software update policy settings in Microsoft Intune.":::

   1. **Select version to install**. You can choose from:

      - *Latest update*: Deploys the most recently released update for iOS/iPadOS.
      - Any previous version that is available in the dropdown box. If you select a previous version, you must also deploy a device configuration policy to [delay visibility](#delay-visibility-of-software-updates) of software updates.

   2. **Schedule type**: Configure the schedule for this policy:

      - *Update at next check-in*: The update installs on the device the next time it checks in with Intune. This option is the simplest and has no extra configurations.
      - *Update during scheduled time*: You configure one or more windows of time during which the update installs upon check-in.
      - *Update outside of scheduled time*: You configure one or more windows of time. During these windows, updates don't install upon check-in.

   3. **Weekly schedule**: If you choose a schedule type other than *update at next check-in*, configure the following options:

      :::image type="content" source="./media/software-updates-ios/scheduled-time.png" alt-text="Screenshot that shows selecting to install an update during scheduled time in an update policy in Microsoft Intune.":::

      - **Time zone**: Choose a time zone.
      - **Time window**: Define one or more blocks of time that restrict when the updates install. The effect of the following options depends on the Schedule type you selected. With a start day and end day, overnight blocks are supported. Options include:

        - **Start day**: Choose the day on which the schedule window starts.
        - **Start time**: Choose the time day when the schedule window begins. For example, you select 5 AM and have a Schedule type of *Update during scheduled time*. In this scenario, 5 AM is the time that updates can begin to install. If you chose a Schedule type of *Update outside of a scheduled time*, then 5 AM is the start of a period of time that updates can't install.
        - **End day**: Choose the day on which the schedule window ends.
        - **End time**: Choose the time of day when the schedule window stops. For example, you select 1 AM and have a Schedule type of *Update during scheduled time*. In this scenario, 1 AM is the time when updates can no longer install. If you chose a Schedule type of *Update outside of a scheduled time*, 1 AM is the start of a period of time that updates can install.

      If you don't configure times to start or end, the configuration results in no restriction and updates can install at any time.

      > [!NOTE]
      >
      > You can configure settings in a [device restrictions](#delay-visibility-of-software-updates) profile to hide an update from device users for a period of time on your supervised iOS/iPadOS devices. A restriction period can give you time to test an update before it's visible to users to install. After the device restriction period expires, the update becomes visible to users. Users can then choose to install it, or your Software update policies might automatically install it soon after.
      >
      > When you use a device restriction to hide an update, review your software update policies to ensure they won't schedule the installation of the update before that restriction period ends. Software update policies install updates based on their own schedule, regardless of the update being hidden or visible to the device user.

   After configuring *Update policy settings*, select **Next**.

5. If [available](../fundamentals/scope-tags.md#default-scope-tag), on the **Scope tags** tab, select **+ Select scope tags** to open the *Select tags* pane if you want to apply them to the update policy.

   - On the **Select tags** pane, choose one or more tags, and then **Select** to add them to the policy and return to the *Scope tags* pane.

   When ready, select **Next** to continue to *Assignments*.

6. On the **Assignments** tab, choose **+ Select groups to include** and then assign the update policy to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. When ready, select **Next** to continue.

   The devices used by the users targeted by the policy are evaluated for update compliance. This policy also supports userless devices.

7. On the **Review + create** tab, review the settings, and then select **Create** when ready to save your iOS/iPadOS update policy. Your new policy is displayed in the list of update policies for iOS/iPadOS.

> [!NOTE]
> You can't use Intune software update policies to downgrade the OS version on a device.

## Edit an existing policy

You can edit an existing policy, including changing the restricted times:

1. Select **Devices** > **Update policies for iOS**. Select the policy you want to edit.

2. While viewing the policies **Properties**, select **Edit** for the policy page you want to modify.

   :::image type="content" source="./media/software-updates-ios/edit-policy.png" alt-text="Screenshot that shows how to edit an existing iOS/iPadOS software update policy in Microsoft Intune.":::

3. After introducing a change, select **Review + save** > **Save** to save your edits, and return to the policies *Properties*.

> [!NOTE]
> If the **Start time** and **End time** are both set to 12 AM, Intune does not check for restrictions on when to install updates. This means that any configurations you have for **Select times to prevent update installations** are ignored, and updates can install at any time.

## Delay visibility of software updates

When you use update policies for iOS, you might have need to delay visibility of an iOS software update. Reasons to delay visibility include:

- Prevent users  from updating the OS manually
- To deploy an older update while preventing users from installing a more recent one

To delay visibility, deploy a device restriction template that configures the following settings:  

- **Defer software updates** = **Yes**  
  This doesn't affect any scheduled updates. It represents days before software updates are visible to end users after release.

- **Delay default visibility of software updates** = **1** to **90**  
  90 days is the maximum delay that Apple supports.

[Device restriction](../configuration/device-restrictions-configure.md) templates are part of device configuration policies.

For guidance from the Intune support team, see the Intune Customer Success blog [Delaying visibility of software updates in Intune for supervised iOS devices](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Delaying-visibility-of-software-updates-in-Intune-for-supervised/ba-p/345753).

## Monitor for update installation failures on devices

In the Microsoft Intune admin center, go to **Devices** > **Monitor** > **Installation failures for iOS devices**.

Intune displays a list of supervised iOS/iPadOS devices that are targeted by an update policy. The list doesn't include devices that are up-to-date and healthy because iOS/iPad devices only return information about installation failures.

For each device on the list, the *Installation Status* displays the error that the device returns. To view the list of potential installation status values, on the *Installation failures for iOS devices* page, select **Filters** and then expand the drop-down list for *Installation Status*.

## Next steps

- [Monitor device profiles](../configuration/device-profile-monitor.md)
- [Software updates admin guide for supervised iOS/iPadOS devices in Intune](software-updates-guide-ios-ipados.md)
