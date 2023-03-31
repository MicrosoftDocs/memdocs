---
# required metadata

title: Use Microsoft Intune policies to manage macOS software updates
description: Use Microsoft Intune to manage system updates for supervised macOS devices.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 04/18/2023
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

# Manage macOS software update policies in Intune

You can use Microsoft Intune to manage software updates for macOS devices that enrolled as [supervised devices](../enrollment/macos-enroll.md#user-approved-enrollment).

This feature applies to:

- macOS 12 and later (supervised)

> [!NOTE]
> Prior to the macOS 12.5 release, devices may download and install additional updates before installing the latest update. 

With policies for macOS software updates, you can:

- Remotely manage how downloads, installations, and notifications should occur when the following types of updates are available for macOS:

  - *Critical update*
  - *Firmware update*
  - *Configuration file update*
  - *All other updates (OS, built-in apps)*

- Specify a schedule that determines when the update installs. Schedules can be as simple as installing updates the next time that the device checks in or creating day-time ranges during which updates can install or are blocked from installing.

By default, devices check in with Intune about every 8 hours. If an update is available through an update policy, the device downloads the update. The device then installs the update upon next check-in within your schedule configuration.

## Configure the policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

    > [!TIP]  
    > For more information on managing software updates and the update experience on devices, see [Manage software updates for Apple devices - Apple Support](https://support.apple.com/en-am/guide/deployment/depafd2fad80/1/web/1.0) at Apple's Platform Deployment site.

2. Select **Devices** > **Update policies for macOS** > **Create profile**.

3. On the **Basics** tab, specify a name for this policy, specify a description (optional), and then select **Next**.

4. On the **Update policy settings** tab, configure the following options:

   :::image type="content" source="./media/software-updates-macos/macos-update-policy-settings.png" alt-text="Screen capture of the Update policy settings page.":::  

   1. For *Critical*, *Firmware*, *Configuration file*, and *All other updates (OS, built-in apps)*, the following installation actions can be configured:

      - **Download and install**: Download or install the update, depending on the current state.

      - **Download only**: Download the software update without installing it.

      - **Install immediately**: Download the software update and trigger the restart countdown notification. This action is recommended for userless devices. 

      - **Notify only**: Download the software update and notify the user through System Settings.

      - **Install later**: Download the software update and install it later. This action is not available for major OS upgrades.

        When you configure *Install later* for *All other updates (OS, built-in-apps), the following additional settings are available:

        - **Max User Deferrals**:  
        When the *All other updates* update type is configured to *Install later*, this setting allows you to specify the maximum number of times a user can postpone a minor OS update before it’s installed. The system prompts the user once a day. Available for devices running macOS 12 and later. 

        - **Priority**: When the *All other updates* update type is configured to *Install later*, this setting allows you to specify values of *Low* or *High* for the scheduling priority for downloading and preparing minor OS updates. Available for devices running macOS 12.3 and later.

      - **Not configured**: No action taken on the software update.

      > [!NOTE]
      > Devices with Apple Silicon require an MDM-issued bootstrap token to authenticate automated, non-interactive updates and upgrades.

   2. **Schedule type**: Configure the schedule for this policy:

      - **Update at next check-in**: The update installs on the device the next time it checks in with Intune. This option is the simplest and has no extra configurations.

      - **Update during scheduled time**: You configure one or more windows of time during which the update will install upon check-in.

      - **Update outside of scheduled time**: You configure one or more windows of time during which the updates won't install upon check-in.

   3. **Weekly schedule**: If you choose a schedule type other than *update at next check-in*, configure the following options:

        :::image type="content" source="./media/software-updates-macos/update-policy-schedule-settings.png" alt-text="Screen capture of the Update policy schedule settings.":::

      - **Time zone**: Choose a time zone.

      - **Time window**: Define one or more blocks of time that restrict when the updates install. The effect of the following options depends on the Schedule type you selected. With a start day and end day, overnight blocks are supported. Options include:

      - **Start day**: Choose the day on which the schedule window starts.

      - **Start time**: Choose the time day when the schedule window begins. For example, if you select 5 AM and have a Schedule type of *Update during scheduled time*, 5 AM will be the time that updates can begin to install. If you chose a Schedule type of *Update outside of a scheduled time*, 5 AM will be the start of a period of time that updates can't install.

      - **End day**: Choose the day on which the schedule window ends.

      - **End time**: Choose the time of day when the schedule window stops. For example, if you select 1 AM and have a Schedule type of *Update during scheduled time*, 1 AM will be the time when updates can no longer install. If you chose a Schedule type of *Update outside of a scheduled time*, 1 AM will be the start of a period of time that updates can install.

   If you don't configure times to start or end, the configuration results in no restriction and updates can be installed at any time.

   > [!TIP]  
   > You can deploy a settings catalog policy to hide an update from device users for a period of time on your supervised macOS devices. For more informtaion see the following section [Delay visibility of updates](#delay-visibility-of-updates).

   <!-- 
   > You can configure settings in a [Settings Catalog](../protect/software-updates-ios.md#delay-visibility-of-software-updates) policy to hide an update from device users for a period of time on your supervised macOS devices. A restriction period can give you time to test an update before it's visible to users to install. After the device restriction period expires, the update becomes visible to users. Users can then choose to install it, or your Software update policies might automatically install it soon after.
   >
   > When you use a device restriction to hide an update, review your software update policies to ensure they won't schedule the installation of the update before that restriction period ends. Software update policies install updates based on their own schedule, regardless of the update being hidden or visible to the device user.
   -->
5. After configuring *Update policy settings*, select **Next**.

6. On the **Scope tags** tab, select **+ Select scope tags** to open the *Select tags* pane if you want to apply them to the update policy.

   - On the **Select tags** pane, choose one or more tags, and then **Select** to add them to the policy and return to the *Scope tags* pane.

   - When ready, select **Next** to continue to *Assignments*.

7. On the **Assignments** tab, choose **+ Select groups to include** and then assign the update policy to one or more groups. Use **+ Select groups to exclude** to fine-tune the assignment. When ready, select **Next** to continue.

   The devices used by the users targeted by the policy are evaluated for update compliance. This policy also supports userless devices.

8. On the **Review + create** tab, review the settings, and then select **Create** when ready to save your macOS update policy. Your new policy is displayed in the list of update policies for macOS.

> [!NOTE]  
> Apple MDM doesn't allow you to force a device to install updates by a certain time or date. You can't use Intune software update policies to downgrade the OS version on a device.

## Delay visibility of updates

When you use update policies for macOS, you might want to hide updates from users of supervised macOS devices for a period of time. You can accomplish this with a settings catalog policy for macOS devices that configure update restriction periods.

A restriction period can give you time to test an update before it’s made available to users to install. After the restriction period ends, the update becomes visible to users, and they can choose to install it if your update policies don’t install it first.

If you use device restrictions to hide an update, review your software update policies to ensure they won’t schedule the installation of that update before the restriction period ends. Software update policies will install updates per their schedule regardless of the update being hidden or visible to the device user.

You’ll find settings that can restrict visibility of updates on macOS devices in the **Restrictions** category of the [settings catalog](../configuration/settings-catalog.md). A few examples of settings you can use to defer an update include:

- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay
- Enforced Software Update Non OS Deferred Install Delay

You can also find related settings under the **System Updates** > **Software Update** category to manage how users manually interact with updates through their system UI. However, updates from a targeted update policy will override these settings.

## Edit a policy

You can edit an existing policy, including changing the restricted times:

1. Select **Devices** > **Update policies for macOS**. Select the policy you want to edit.
2. While viewing the policies **Properties**, select **Edit** for the policy page you want to modify.

   :::image type="content" source="./media/software-updates-macos/edit-a-macos-update-policy.png" alt-text="Screen capture of the policy edit page.":::

3. After introducing a change, select **Review + save** > **Save** to save your edits.

> [!NOTE]  
> If the **Start time** and **End time** are both set to 12 AM, Intune does not check for restrictions on when to install updates. This means that any configurations you have for **Select times to prevent update installations** are ignored, and updates can install at any time.

## Configure additional macOS software update settings using the Settings Catalog

The *Restrictions* category contains the following settings that can be used to delay visibility of macOS software updates on devices (**Devices** > **macOS** > **Device configuration** > **Settings catalog** > **Restrictions**):

- *Enforced Software Update Delay*:  Sets how many days to delay a software update on the device. With this restriction in place, the user doesn’t see a software update until the specified number of days after the software update release date. This value is used by *Force Delayed App Software Updates* and *Force Delayed Software Updates*.

- *Force Delayed App Software Updates*:  If true, delays user visibility of non-OS Software Updates for built-in software like Safari, XProtect, and Gatekeeper. Requires a supervised device. The delay is 30 days unless *Enforced Software Update Delay* is set to another value.

- *Enforced Software Update Non OS Deferred Install Delay*:  This restriction allows the admin to set how many days to delay an app software update on the device. When this restriction is in place, the user sees a non-OS software update only after the specified delay after the release of the software. This value controls the delay for Force Delayed App Software Updates.

- *Force Delayed Major Software Updates*:  If set to true, delays user visibility of major upgrades to OS Software.

- *Enforced Software Update Major OS Deferred Install Delay*:  This restriction allows the admin to set how many days to delay a major software upgrade on the device. Major software upgrades are new major OS releases; for example, macOS 12 Monterrey and macOS 13 Ventura. When this restriction is in place, the user sees a software upgrade only after the specified delay after the release of the software upgrade. This value controls the delay for *Force Delayed Major Software Updates*.

- *Force Delayed Software Updates*:  If true, delays user visibility of software updates. In macOS, seed build updates are allowed, without delay. The delay is 30 days unless *Enforced Software Update Delay* is set to another value.

- *Enforced Software Update Minor OS Deferred Install Delay*:  This restriction allows the admin to set how many days to delay a minor OS software update on the devices. Minor software updates are intermediate updates that are released between major OS upgrades; for example, macOS 13.1 and macOS 13.2. When this restriction is in place, the user sees a software update only after the specified delay after the release of the software update. This value controls the delay for *Force Delayed Software Updates*.

The Software Update category contains the following settings that can be used to configure the user experience for macOS software update options on devices (**Devices** > **macOS** > **Device configuration** > **Settings catalog** > **System Updates** > **Software Update**):

- *Allow Pre Release Installation*:  If true, prerelease software can be installed on this computer.

- *Automatic Check Enabled*:  If false, deselects the "Check for updates" option and prevents the user from changing the option.

- *Automatic Download*:  If false, deselects the "Download new updates when available from the App Store" option and prevents the user from changing the option.

- *Automatically Install App Updates*:  If false, deselects the "Install app updates from the App Store" option and prevents the user from changing the option.

- *Automatically Install macOS Updates*:  If false, restricts the "Install macOS Updates" option and prevents the user from changing the option.

- *Config Data Install*:  If false, restricts the automatic installation of configuration data.

- *Critical Update Install*:  If false, disables the automatic installation of critical updates and prevents the user from changing the "Install system data files and security updates" option.

- *Restrict Software Update Require Admin To Install*:  If true, restrict app installations to admin users. This key has the same function as the Restrict Store Require Admin To Install setting in the App Store category.

## Monitor for update installation failures on devices

In the Microsoft Intune admin center, go to **Devices** > **Monitor** > **Installation status for macOS devices**.

Intune displays a list of supervised macOS devices that are targeted by an update policy. The list doesn't include devices that are up-to-date and healthy because macOS devices only return information about installation failures.

For each device on the list, the Installation Status displays the error that was returned by the device. To view the list of potential installation status values, on the *Installation status  for macOS devices* page, select **Filters** and then expand the drop-down list for *Installation Status*.

## Next steps

[Monitor device profiles](../configuration/device-profile-monitor.md)
