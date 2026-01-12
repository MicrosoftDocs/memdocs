---
title: Windows Update settings you can manage with Intune Update Ring policies for Windows devices.
description: View the settings for Windows Update that you can manage through Intune policy for Update rings.
ms.date: 01/12/2026
ms.topic: reference
ms.reviewer: davguy; bryanke
---


# Update rings policy settings

Update rings policies in Microsoft Intune provide a set of configurable settings that control how Windows updates are delivered and installed on managed devices. These settings allow administrators to tailor the update experience to meet organizational needs, balancing update compliance with user productivity.

The policy settings are divided into two main categories: **Update settings** and **User experience settings**.

## Update settings

Update settings control what bits a device will download, and when.

:::row:::
    :::column span="1":::
    **Microsoft product updates**
    :::column-end:::
    :::column span="3":::
    > - **Allow**: To scan for app updates from Microsoft Update.
    > - **Block**: To prevent scanning for app updates.
    >
    > Configuration service provider (CSP) reference: [AllowMUUpdateService](/windows/client-management/mdm/policy-csp-update#allowmuupdateservice).
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Windows drivers**
    :::column-end:::
    :::column span="3":::
    > - **Allow** - To include Windows Update drivers during updates.
    > - **Block** - To prevent scanning for drivers.
    >
    > Configuration service provider (CSP) reference: [ExcludeWUDriversInQualityUpdate](/windows/client-management/mdm/policy-csp-update#excludewudriversinqualityupdate).
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Quality update deferral period (days)**
    :::column-end:::
    :::column span="3":::
    > Specify the number of days from 0 to 30 for which quality updates are deferred. This period is in addition to any deferral period that is part of the service channel you select.
    >
    > The deadline calculation for both quality and feature updates is based off the time the client's update scan initially discovered the update. See [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).
    > 
    >Configuration service provider (CSP) reference: [DeferQualityUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferqualityupdatesperiodindays).
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Feature update deferral period (days)**
    :::column-end:::
    :::column span="3":::
    > Specify the number of days from 0 to 365 for which feature updates are deferred. This period is in addition to any deferral period that is part of the service channel you select. The deferral period begins when Microsoft releases the update.
    >
    > Configuration service provider (CSP) reference: [DeferFeatureUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferfeatureupdatesperiodindays).
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Upgrade Windows 10 devices to Latest Windows 11 release**
    :::column-end:::
    :::column span="3":::
    > When set to *Yes*, eligible Windows 10 devices will upgrade to the most current Windows 11 release.
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Set feature update uninstall period (2 - 60 days)**
    :::column-end:::
    :::column span="3":::
    > Configure a time after which feature updates can't be uninstalled. After this period expires, the previous update bits are removed from the device, and it can no longer uninstall to a previous update version.
    >
    >For example, consider an update ring with a feature update uninstall period of 20 days. After 25 days, you decide to roll back the latest feature update and use the *Uninstall* option. Devices that installed the feature update over 20 days ago can't uninstall it as they've removed the necessary bits as part of their maintenance. However, devices that only installed the feature update up to 19 days ago can uninstall the update if they successfully check in to receive the uninstall command before exceeding the 20-day uninstall period.
    >
    >Configuration service provider (CSP) reference: [ConfigureFeatureUpdateUninstallPeriod](/windows/client-management/mdm/policy-csp-update#configurefeatureupdateuninstallperiod).
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Enable pre-release builds**
    :::column-end:::
    :::column span="3":::
    > When enabled, targeted devices will move to the pre-release build you specify. You must specify one of the following prerelease builds:
    >- **Windows Insider - Release Preview**
    >- **Beta Channel**
    >- **Dev Chanel**
    >
    > For information about pre-release builds, see [Windows Insider](https://insider.windows.com/understand-flighting).
    >
    >Configuration service provider (CSP) reference: [BranchReadinessLevel](/windows/client-management/mdm/policy-csp-update#branchreadinesslevel).
    :::column-end:::
:::row-end:::

## User experience settings

User experience settings control the end-user experience for device restart and reminders.

:::row:::
    :::column span="1":::
    **Automatic update behavior**
    :::column-end:::
    :::column span="3":::
    > Choose how automatic updates are installed and, if necessary, when to restart the device:
    >
    >- **Notify download**: Notify the user before downloading the update. Users choose to download and install updates. If the user takes no action, the update will not install until the deadline you have configured is reached.
    >- **Auto install at maintenance time**: Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, users are prompted to restart for up to seven days, and then restart is forced. This option can restart a device automatically after the update installs.
    >
    >   Use the **Active hours** settings to define a period during which the automatic restarts are blocked:
    >   - **Active hours start**: Specify a start time for suppressing restarts due to update installations.
    >   - **Active hours end**: Specify an end time for suppressing reboots due to update installations.
    >- **Auto install and restart at maintenance time**: Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used, which is the default for unmanaged devices.\
    >  This option can restart a device automatically after the update installs. **Active hours** settings are used to define a period during which the automatic restarts are blocked:
    >   - **Active hours start** - Specify a start time for suppressing restarts due to update installations.
    >   - **Active hours end**: Specify an end time for suppressing reboots due to update installations.
    >
    >- **Auto install and restart at a scheduled time**: Specify an installation day and time. If unspecified, installation runs at 3 AM daily, followed by a 15-minute countdown to a restart. Logged on users can delay countdown and restart. When set to *Auto install and restart at a scheduled time*, you can configure the following settings:
    >  - **Automatic behavior frequency** - Use this setting to schedule when updates are installed, including the week, the day, and the time.
    >  - **Scheduled install day** - Specify on which day of the week you want updates to install.
    >  - **Scheduled install time** - Specify the time of day when you want updates to install.
    >>[!NOTE]
    >>The device might not complete the installation at the specified time because of power policies, user absence, and so on. In this case, it will not attempt installation until the specified time occurs again or until a deadline you have specified is reached.
    >- **Auto install and reboot without end-user control** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used. This option sets the end-users control pane to read-only.
    >- **Reset to default** - Restore the original auto update settings. When you *reset to default*, Windows will automatically determine active hours for the device. Using the active hours, Windows then schedules the best time to install updates and restart the system after updates install.
    >Configuration service provider (CSP) reference:
    > - [AllowAutoUpdate](/windows/client-management/mdm/policy-csp-update#allowautoupdate)
    > - [ActiveHoursStart](/windows/client-management/mdm/policy-csp-update#activehoursstart)
    > - [ActiveHoursEnd](/windows/client-management/mdm/policy-csp-update#activehoursend)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Restart checks (EDU Restart)**
    :::column-end:::
    :::column span="3":::
    >- **Allow**: Perform restart checks: Battery level = 40%, User presence, Display Needed, Presentation mode, Full screen mode, phone call state, game mode etc.
    >- **Skip**: Will restrict updates to download and install outside of Active Hours. Updates will be allowed to start even if there is a signed-in user or the device is on battery power, providing there is more than 70% battery capacity. Windows will schedule the device to wake from sleep 1 hour after the [Active Hours End](/windows/client-management/mdm/policy-csp-update#activehoursend) time with a 60-minute random delay. Devices will reboot immediately after the updates are installed. If there are still pending updates, the device will continue to retry every hour for 4 hours.<br><br>This option is designed for education devices that remain in carts overnight that are left in sleep mode. It is not designed for 1:1 devices.
    >>[!NOTE]
    >>In policies where this value is currently set to *Skip*, the value will remain in place until that value is changed to *Allow* and saved. However, When creating new policies, it will not be available, and you can use [Settings catalog](../../intune-service/configuration/settings-catalog.md) to set this value if required.
    >
    >Configuration service provider (CSP) reference: [SetEDURestart](/windows/client-management/mdm/policy-csp-update#setedurestart)
    :::column-end:::
:::row-end:::


:::row:::
    :::column span="1":::
    **Option to pause Windows updates**
    :::column-end:::
    :::column span="3":::
    >- **Enable**: Allow device users to pause the installation of an update for a certain number of days.
    >- **Disable**: Prevent device users from pausing the installation of an update.
    >
    >Configuration service provider (CSP) reference: [SetDisablePauseUXAccess](/windows/client-management/mdm/policy-csp-update#setdisablepauseuxaccess)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Option to check for Windows updates**
    :::column-end:::
    :::column span="3":::
    >- **Enable**: Allow device users to use Windows Update scan to find updates.
    >- **Disable**: Prevent device users from accessing the Windows Update scan.
    >
    >Configuration service provider (CSP) reference: [SetDisableUXWUAccess](/windows/client-management/mdm/policy-csp-update#setdisableuxwuaccess)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
    **Change notification Update level**
    :::column-end:::
    :::column span="3":::
    >Specify what level of Windows Update notifications users see. This setting doesn't control how and when updates are downloaded and installed.<br><br>Supported options:
    >- **Not configured**
    >- **Use the default Windows Update notifications**
    >- **Turn off all notifications, excluding restart warnings**
    >- **Turn off all notifications, including restart warnings**
    >
    >Configuration service provider (CSP) reference: [UpdateNotificationLevel](/windows/client-management/mdm/policy-csp-update#updatenotificationlevel)
:::row-end:::

:::row:::
    :::column span="1":::
    **Use deadline settings**
    :::column-end:::
    :::column span="3":::
    >Enables the configuration of deadline settings:
    >- **Not configured**
    >- **Allow**
    >
    >When set to *Allow*, you can configure the following settings for deadlines:
    > **Deadline for feature updates**: Specifies the number of days a user has before feature updates are installed on their devices automatically (2-30).
    > **Deadline for quality updates**: Specifies the number of days a user has before quality updates are installed on their devices automatically (2-30).
    > **Grace period**: Specifies a minimum number of days after deadline until restarts occur automatically (0-7).
    > **Auto reboot before deadline**: Specifies whether the device will attempt to automatically reboot outside of active hours before the deadline and grace period are expired. The recommended value is **Yes**, as it enables the system to reboot when the user isn't using the device. Setting this value to **No** forces the system to wait until the deadline and grace period are expired and then restarts the device and this could occur during active hours.
    >
    >For more details about how deadlines and grace periods work together see [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).
    >
    >Configuration service provider (CSP) reference:
    > - [ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforfeatureupdates)
    > - [ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforqualityupdates)
    > - [ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiod)
    > - [ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot)
:::row-end:::
