---
title: Device restart notifications
titleSuffix: Configuration Manager
description: Restart notification behavior for various client settings in Configuration Manager.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Device restart notifications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The notifications a user receives for a pending device restart can vary depending on the [Computer restart client settings](#client-settings) and which version of Configuration Manager you use. This article helps you configure the user experience for pending device restart notifications.

> [!NOTE]
> By default, Windows 11 enables **focus assist** for the first hour after a user signs on for the first time. For more information, see [Reaching the Desktop and the Quiet Period](/windows-hardware/customize/desktop/customize-oobe-in-windows-11#reaching-the-desktop-and-the-quiet-period).
>
> Software Center notifications are currently suppressed during this time. For more information, see [Turn Focus assist on or off in Windows](https://support.microsoft.com/windows/turn-focus-assist-on-or-off-in-windows-5492a638-b5a3-1ee0-0c4f-5ae044450e09#ID0EBD=Windows_11).<!-- 11059565 -->

## Deployment types for restart notifications

The [Computer restart client settings](#client-settings) change the user experience for all required deployments that require a restart of the following types:

- [Application](../../../apps/deploy-use/deploy-applications.md)
- [Task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md)
- [Software update](../../../sum/deploy-use/deploy-software-updates.md)

## Restart notification types

When a device requires a restart, the client shows a notification to the end user of the upcoming restart.

### Toast notification

A Windows toast notification informs the user that the device needs to restart. The information in the toast notification can be different depending on which version of Configuration Manager you're running. This type of notification is native to the Windows OS. You may also see third-party software using this type of notification.

:::image type="content" source="media/3555947-restart-toast.png" alt-text="Toast notification of pending restart":::

### Software Center notification with snooze

Software Center shows a notification with a snooze option and the time remaining before it forces the devices to restart. The message may be different depending on your version of Configuration Manager.

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="Pending restart Software Center notification with snooze button":::

### Software Center final countdown notification

Software Center shows this final countdown notification that the user can't close or snooze. The user won't see a progress bar in the restart notification until the pending restart is less than 24 hours away.


:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="Software Center final restart countdown":::

### Software Center notification before deadline

If the user proactively installs required software before the deadline, and it requires a restart, they'll see a different notification. The following notification occurs when both the user experience setting allows notifications and you don't use toast notifications for the deployment. For more information about configuring these settings, see [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) and [User notifications for required deployments](../../../apps/plan-design/user-notifications.md).

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Notification for proactively installed software":::

#### Available apps

When you don't use toast notifications, the dialog for software marked as **Available** is similar to proactively installed software. For **Available** software, the notification doesn't have a deadline for the restart and the user can choose their own snooze interval. For more information, see [Approval settings](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="Available software doesn't have a deadline for restart in the notification":::

### Software Center notification of required restart

<!--3601213-->

You can configure client settings to prevent devices from automatically restarting when a deployment requires it. When a required deployment needs the device to restart, but you disable the client setting **Configuration Manager can force a device to restart**, you see the following notification:

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="Software Center notification to restart your computer":::

If you **Snooze** this notification, it will show again based on how you configure the frequency of restart reminder notifications. The device won't restart until you select **Restart** or manually restart Windows.

> [!NOTE]
> By default, Configuration Manager can still force devices to restart.

## Client settings

To control the client restart behaviors, configure the following device client settings in the **Computer Restart** group. For more information, see [How to configure client settings](configure-client-settings.md).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also updated.

### Configuration Manager can force a device to restart

<!--3601213-->

You can configure client settings to prevent devices from automatically restarting when a deployment requires it. Configuration Manager enables this setting by default.

> [!IMPORTANT]
> This client setting applies to all application, software update, and package deployments to the device. Until a user manually restarts the device:
>
> - Software updates and app revisions may not be fully installed
> - Additional software installs may not happen

When you disable this setting, you can't specify the amounts of time after the deadline that the device is restarted or the user is presented a final countdown notification.


### Specify the amount of time after the deadline before a device gets restarted (minutes)

This setting must be shorter in duration than the shortest maintenance window applied to the computer. For more information about maintenance windows, see [How to use maintenance windows](../manage/collections/use-maintenance-windows.md).

The default value is 90 minutes. The maximum value is 20160 minutes (two weeks).

> [!NOTE]
> This setting was previously titled **Display a temporary notification to the user that indicates the interval before the user is logged off or the computer restarts (minutes)**.

### Specify the amount of time that a user is presented a final countdown notification before a device gets restarted (minutes)

This setting must be shorter in duration than the shortest maintenance window applied to the computer. For more information about maintenance windows, see [How to use maintenance windows](../manage/collections/use-maintenance-windows.md).

The default value is 15 minutes.

> [!NOTE]
> This setting was previously titled **Display a dialog box that the user cannot close, which displays the countdown interval before the user is logged off or the computer restarts (minutes)**.

### Specify the frequency of reminder notifications presented to the user, after the deadline, before a device gets restarted (minutes)
<!--3976435-->

This frequency duration value should be less than the value of **Specify the amount of time after the deadline before a device gets restarted (minutes)** minus the value of **Specify the amount of time that a user is presented a final countdown notification before a device gets restarted (minutes)**. Otherwise, the reminder notifications won't work.

The default value is 240 minutes.

> [!NOTE]
> This setting was previously titled **Specify the snooze duration for computer restart countdown notifications (minutes)**.

### When a deployment requires a restart, show a dialog window to the user instead of a toast notification
<!--3555947-->
To change the user experience to be more intrusive, configure this setting to **Yes**. This setting applies to all deployments of applications, task sequences, and software updates. For more information, see [User notifications](../../../apps/plan-design/user-notifications.md#replace-toast-notifications-with-dialog-window).

### When a deployment requires a restart, allow low-rights users to restart a device running Windows Server

<!--7821529-->

For a low-rights user on a device that runs Windows Server, by default they aren't assigned the user rights to restart Windows. When you target a deployment to this device, this user can't manually restart. For example, they can't restart Windows to install software updates.

> [!IMPORTANT]
> Allowing low-rights users to restart a server can potentially impact other users or services.


## Device restart notifications
<!--3976435-->
Some customers prefer frequent restart notifications and allowing users a short time frame to postpone. Others allow users to postpone a restart for longer periods of time, and infrequently notify users of the pending restart. You have control over the timing and frequency of restart notifications.

### Install required software at or after the deadline

When required software is installed at or after the deadline, your users will see notifications depending on what client settings you selected.

If the setting **When a deployment requires a restart, show a dialog window to the user instead of a toast notification** is set to:

- **No**: Windows shows toast notifications until the deployment reaches the final countdown notification.

- **Yes**: Software Center shows a notification:

  - If the restart is greater than 24 hours away, it shows an estimated restart time. The timing of this notification is based on the setting: **Specify the amount of time after the deadline before a device gets restarted (minutes)**.

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="Restart time is greater than 24 hours away":::

  - If the restart is less than 24 hours away, it shows a progress bar. The timing of this notification is based on the setting: **Specify the amount of time after the deadline before a device gets restarted (minutes)**.

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="Restart time is less than 24 hours away":::

If the user selects **Snooze**, another temporary notification shows after the snooze period elapses. This behavior assumes it hasn't yet reached the final countdown. The timing of the next notification is based on the setting: **Specify the frequency of reminder notifications presented to the user, after the deadline, before a device gets restarted (minutes)**. If the user selects **Snooze**, and your snooze interval is one hour, then Software Center notifies the user again in 60 minutes. This behavior assumes it hasn't yet reached the final countdown.

When it reaches the final countdown, Software Center shows the user a notification they can't close. The progress bar is in red and the user can't **Snooze** it.

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="Software Center final countdown notification":::

### Proactively install required software before the deadline

If the user proactively installs required software that needs restart before the deadline, they'll see a different notification. For more information about configuring these settings, see [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) and [User notifications for required deployments](../../../apps/plan-design/user-notifications.md).

The following notification occurs when both the user experience setting allows notifications and you don't use toast notifications for the deployment:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Notification for proactively installed software":::

Once the deployment reaches its deadline, Software Center follows the behavior to [Install required software at or after the deadline](#install-required-software-at-or-after-the-deadline).

## Example configurations

The following examples describe how to configure the client settings to achieve specific behaviors.

> [!NOTE]
> If the user puts the device to sleep, it doesn't pause or interrupt a countdown. For example, a restart countdown is halfway into a four-hour timer, and the user puts the device to sleep. 12 hours later the user wakes up the device. The device restarts, as it's past the deadline.<!-- SCCMDocs#2295 -->

### Reminders are off

| Setting | Value |
|---------|---------|
|Specify the amount of time after the deadline before a device gets restarted (minutes)|180|
|Specify the amount of time that a user is presented a final countdown notification before a device gets restarted (minutes)|60|
|Specify the frequency of reminder notifications presented to the user, after the deadline, before a device gets restarted (minutes)|240|
|When a deployment requires a restart, show a dialog window to the user instead of a toast notification|No|

The device will restart three hours (**180** minutes) after the deployment deadline. One hour (**60** minutes) before it restarts, the user sees a countdown that they can't close or snooze. The first reminder notification is set to start four hours (**240** minutes) after the deadline, which is after the restart. So the user doesn't see any reminders.

### Low reminder frequency

| Setting | Value |
|---------|---------|
|Specify the amount of time after the deadline before a device gets restarted (minutes)|7200|
|Specify the amount of time that a user is presented a final countdown notification before a device gets restarted (minutes)|120|
|Specify the frequency of reminder notifications presented to the user, after the deadline, before a device gets restarted (minutes)|900|
|When a deployment requires a restart, show a dialog window to the user instead of a toast notification|Yes|

The device will restart five days (**7200** minutes) after the deployment deadline. Two hours (**120** minutes) before it restarts, the user sees a countdown that they can't close or snooze. This configuration allows for 118 hours to show reminders (`(7200 - 120) / 60`). 15 hours (**900** minutes) after the deadline, Software Center displays the first reminder. It displays a maximum of six additional reminders every 15 hours (**900 minutes**). The user sees the reminder as a window on the screen, instead of a notification that disappears in a few seconds.

### High reminder frequency

| Setting | Value |
|---------|---------|
|Specify the amount of time after the deadline before a device gets restarted (minutes)|2880|
|Specify the amount of time that a user is presented a final countdown notification before a device gets restarted (minutes)|60|
|Specify the frequency of reminder notifications presented to the user, after the deadline, before a device gets restarted (minutes)|30|
|When a deployment requires a restart, show a dialog window to the user instead of a toast notification|Yes|

The device will restart two days (**2880** minutes) after the deployment deadline. One hour (**60** minutes) before it restarts, the user sees a countdown that they can't close or snooze. This configuration allows for 47 hours to show reminders (`(2880 - 60) / 60`). **30** minutes after the deadline, Software Center displays the first reminder. It displays a maximum of 92 additional reminders every **30 minutes**. The user sees the reminder as a window on the screen, instead of a notification that disappears in a few seconds.

## Log files

To troubleshoot device restarts, use the **RebootCoordinator.log** and **SCNotify.log** files on the client. Based on the specific type of deployment, you may also have to use additional client [log files](../../plan-design/hierarchy/log-files.md).

## Next steps

- [How to configure client settings](configure-client-settings.md)
- [Application deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [User notifications for required app deployments](../../../apps/plan-design/user-notifications.md)
