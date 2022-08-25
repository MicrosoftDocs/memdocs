---
title: Use maintenance windows
titleSuffix: Configuration Manager
description: Use collections and maintenance windows to effectively manage clients in Configuration Manager.
ms.date: 08/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
---

# How to use maintenance windows in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use maintenance windows to define when Configuration Manager can run impacting tasks on devices. Maintenance windows help make sure that client configuration changes occur during times that don't affect productivity. With Software Center, users can see the device's next maintenance window on the **Installation status** tab. <!--1358131-->

The following tasks support maintenance windows:

- Application and package deployments

- Software update deployments

- Compliance settings deployment and evaluation

- OS and custom task sequence deployments

Configure maintenance windows with an effective date, a start and end time, and a recurrence pattern. The maximum duration of a window has to be less than 24 hours. The console doesn't allow a single maintenance window longer than 24 hours. For example, if you want to allow maintenance all day Saturday and Sunday, then create two 24-hour maintenance windows for each day.<!-- MEMDocs#310 -->

By default, computer restarts caused by a deployment aren't allowed outside of a maintenance window, but you can override the default. Maintenance windows affect only the time when the deployment runs. Deployments that you configure to download and run locally can download content outside of the window.

When a client is a member of a device collection that has a maintenance window, a deployment runs only if its maximum allowed run time doesn't exceed the duration of the window. If the deployment fails to run, the client generates an alert. It then reruns the deployment during the next scheduled maintenance window that has available time.

> [!TIP]
> A _maintenance window_ is for a client. A _service window_ is for a site server. For more information, see [Service windows for site servers](../../../servers/manage/service-windows.md).

## Multiple maintenance windows

When a client computer is a member of multiple device collections that have maintenance windows, these rules apply:  

- If the maintenance windows don't overlap, the client treats them as two independent maintenance windows.

- If the maintenance windows overlap, the client treats them as a single window for the entire time of both windows. For example, you create two maintenance windows on a collection. The first is effective from 6:00 to 7:00, and the second is effective from 6:30 to 7:30. Because they overlap by 30 minutes, the effective duration of the combined maintenance window is 90 minutes from 6:00 to 7:30.

When a user installs an application from Software Center, the client starts it immediately. It prioritizes the user's intent over the administrator's.

If an application deployment with a purpose of **Required** reaches its installation deadline during the non-business hours that a user configures in Software Center, the client installs the application. It prioritizes the administrator's intent over the user's.

By default, with multiple maintenance windows, the client only installs software updates during **Software Update** type windows. It ignores any **All deployments** maintenance windows, unless they're the only type. You can configure this behavior with the following client setting in the **Software updates** group: **Enable installation of software updates in "All deployments" maintenance window when "Software Update" maintenance window is available**. For more information, see [About client settings](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> This setting also applies to maintenance windows that you configure to apply to **Task sequences**.<!-- SCCMDocs-pr #4596 -->
>
> If the client only has an **All deployments** window available, it still installs software updates or task sequences in that window.

## Configure maintenance windows

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.

1. Select the **Device Collections** node, and then select a collection.

    > [!NOTE]
    > You can't create maintenance windows for the **All Systems** collection.

1. On the **Home** tab of the ribbon, in the **Properties** group, choose **Properties**.

1. Switch to the **Maintenance Windows** tab, and select the **New** icon.

    1. Specify a **Name** to uniquely identify this maintenance window for the collection.

    1. Configure the **Time** settings:

        - **Effective date**: The date when the maintenance windows starts. The default is the current date.

        - **Start** and **End**: The start and end times of the maintenance window. It calculates the **Duration** for the window. The minimum duration is five minutes, and the maximum is 24 hours. The default duration is three hours, from 01:00 to 04:00.

        - **Coordinated Universal Time (UTC)**: Enable this option for the client to interpret the start and end times in the UTC time zone. For regionally or globally distributed devices in the same collection, this option sets the maintenance window to occur simultaneously on all devices in the collection. Disable this option for the client to use the device's local time zone. This option is disabled by default.

    1. Configure the recurrence pattern. The default is once per week on the current day of the week.
        > [!NOTE]
        > Starting in version 2207, you can offset monthly maintenance window schedules to better align deployments with the release of monthly security updates. For example, using an offset of two days after the second Tuesday of the month, sets the maintenance window for Thursday. <!--3601127-->

    1. **Apply this schedule to**: By default the window applies to **All deployments**. You can select either **Software updates** or **Task sequences** to further control what deployments run during this window.

        > [!TIP]
        > If you configure multiple maintenance windows of different types on the same collection, make sure you understand the client behaviors. For more information, see [Multiple maintenance windows](#multiple-maintenance-windows).

1. Select **OK** to save and close the window.


The **Maintenance Windows** tab of the collection properties displays all configured windows.

## <a name="bkmk_powershell"></a> Use PowerShell

You can use PowerShell to configure maintenance windows. For more information, see the following articles:

- [Get-CMMaintenanceWindow](/powershell/module/configurationmanager/get-cmmaintenancewindow)
- [New-CMMaintenanceWindow](/powershell/module/configurationmanager/new-cmmaintenancewindow)
- [Remove-CMMaintenanceWindow](/powershell/module/configurationmanager/remove-cmmaintenancewindow)
- [Set-CMMaintenanceWindow](/powershell/module/configurationmanager/set-cmmaintenancewindow)
