---
title: Deploy configuration baselines
description: Deploy configuration baselines to define configuration baseline deployments and to add or remove configuration baselines from deployments.
ms.date: 10/06/2016
ms.subservice: compliance
ms.topic: install-set-up-deploy
ms.collection: tier3
ms.service: microsoft-endpoint-configuration-manager
---
# How to deploy configuration baselines in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration baselines in Configuration Manager must be deployed to one or more collections of users or devices before client devices in those collections can assess their compliance with the configuration baseline.

Use the **Deploy Configuration Baselines** dialog box to define configuration baseline deployments, which includes adding or removing configuration baselines from deployments in addition to specifying the evaluation schedule.

## Deploy a configuration baseline

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Baselines**.

2.  In the **Configuration Baselines** list, select the configuration baseline that you want to deploy, and then in the **Home** tab, in the **Deployment** group, click **Deploy**.

3.  In the **Deploy Configuration Baselines** dialog box, select the configuration baselines that you want to deploy in the **Available configuration baselines** list. Click **Add** to add these to the **Selected configuration baselines** list.

    > [!IMPORTANT]
    >  If you change a configuration item that has been added to a deployed configuration baseline, the revised configuration item is not evaluated for compliance until its next scheduled evaluation time.

4.  Specify the following additional information:

    -   **Remediate noncompliant rules when supported** – Automatically remediates any rules that are noncompliant for Windows Management Instrumentation (WMI), the registry, scripts, and all settings for mobile devices that are enrolled by Configuration Manager.

    -   **Allow remediation outside the maintenance window** – If a maintenance window has been configured for the collection to which you are deploying the configuration baseline, enable this option to let compliance settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).

5.  **Generate an alert** – Configures an alert that is generated if the configuration baseline compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.

6.  **Collection** - Click **Browse** to select the collection where you want to deploy the configuration baseline.

7.  **Specify the compliance evaluation schedule for this configuration baseline** Specifies the schedule by which the deployed configuration baseline is evaluated on client computers. This can be either a simple or a custom schedule.  

    > [!NOTE]
    > **When the client actually evaluates the baseline**
    >
    > - **Computer-targeted deployments.** After the first evaluation on a given client, the baseline is evaluated within a 2-hour randomization window of each scheduled start time. The **first** evaluation on a Windows client device is additionally gated by two launch conditions: the device must be on power (above the low-battery threshold) and the user must be idle. If either condition isn't met at the scheduled time, the first evaluation is deferred until both become true, or until an internal 24-hour deadline elapses, whichever happens first. On Windows Server, the idle check is skipped, so the first evaluation also runs within the 2-hour window.
    > - **User-targeted deployments.** The baseline is evaluated the next time the target user signs in to a client that has received the deployment policy. The 2-hour randomization window doesn't apply to user-targeted deployments.
    >
    > For details and how to confirm the client-side behavior in `Scheduler.log`, see [How the Configuration Manager client evaluates a deployed baseline](#how-the-configuration-manager-client-evaluates-a-deployed-baseline).

8. Click **OK** to close the **Deploy Configuration Baselines** dialog box and to create the deployment. For more information about how to monitor the deployment, see [Monitor compliance settings](monitor-compliance-settings.md).

## How the Configuration Manager client evaluates a deployed baseline

The evaluation time you configure in the deployment ("Simple schedule" or "Custom schedule") is a *target* time — it isn't a guaranteed run time. The Configuration Manager client applies **launch conditions** and a **2-hour randomization window** on top of your schedule. Understanding these helps you reconcile the schedule you set in the console with what actually happens on the client — which you can inspect in `Scheduler.log`, and, to a lesser extent, in the **Configuration Manager Support Center** client tool.

### Launch conditions

Every scheduled evaluation of a baseline carries two launch conditions:

| Condition | How the client determines it |
|---|---|
| Battery above the low threshold | On a laptop, the battery must be higher than the Windows "low battery" level, or the device must be on AC power. Devices without a battery (desktops, servers) always satisfy this. |
| User is idle | Determined by a hidden Windows Task Scheduler task the Configuration Manager client installs during setup. See [How the client determines idle state](#how-the-client-determines-idle-state). |

If both conditions are met when the trigger fires, the evaluation runs within the built-in **2-hour randomization window** of the scheduled start time.

If either condition isn't met, the evaluation is placed in a pending queue on the client. It runs as soon as the conditions become true (the client is notified when the user goes idle or the device is plugged in), or when an internal **24-hour (1440-minute) deadline** is reached — whichever happens first.

#### How the client determines idle state

The Configuration Manager client doesn't measure idle state directly. Instead, at client installation on **Windows client** editions, setup registers a hidden Windows Task Scheduler task:

```
\Microsoft\Configuration Manager\Configuration Manager Idle Detection
```

The task has the following characteristics:

- **Trigger**: `On idle` (`TASK_TRIGGER_IDLE`) — Windows Task Scheduler fires the task when its own idle heuristics report the machine as idle.
- **Stop when the machine is no longer idle**: enabled. When Windows reports the machine as no longer idle, the task is stopped.
- **Runs on battery**: yes — the task deliberately doesn't restrict itself to AC power, because Windows Task Scheduler itself governs whether idle work should run based on the current power state.
- **Runs as**: `SYSTEM`, hidden.
- **Action**: invokes a COM handler in the Configuration Manager client agent, which flips the client's cached idle state to "idle" while the task is running and to "not idle" when the task stops.

Because the trigger is a standard Windows idle trigger and the client doesn't override the trigger's `IdleDuration` or `WaitTimeout`, the definition of "idle" is the one used by Windows Task Scheduler itself — that is, low CPU and disk activity combined with no user input for the interval configured in Windows. For a full description of how Windows Task Scheduler decides a machine is idle, see [Task Idle Conditions](/windows/win32/taskschd/task-idle-conditions).

> [!NOTE]
> - The idle launch condition is enforced on Windows client devices and not on Windows Server.  
> - For **Windows client devices with continuously active users,** If a user is signed in and using the device throughout the scheduled evaluation window (moving the mouse, typing, running CPU-intensive work), Windows Task Scheduler may never fire the idle trigger, so the client never reports "idle" and the first evaluation is deferred until the 24-hour deadline elapses.

### Why first-run timing differs from subsequent runs

Although launch conditions are checked on **every** scheduled evaluation, the client also keeps a per-schedule history of the previous pending-queue wait. If the elapsed time since the last time the schedule was pending is already greater than the 24-hour deadline (which is the case for any recurring schedule of daily or longer cadence), the client shortens the pending timer to one minute and lets the schedule fire without waiting for the launch conditions to become true.

The net effect for administrators:

- **First evaluation on a given client.** No prior history exists, so the full 24-hour deadline applies. On a Windows client device where a user is actively signed in at the scheduled time, the first evaluation can be delayed by up to 24 hours.
- **All subsequent evaluations.** The client's history of the previous wait shortens the pending timer to one minute, so the evaluation runs within the 2-hour randomization window regardless of user presence or power state.
- **Windows Server.** The idle check is skipped entirely, so every evaluation — including the first — runs within the 2-hour window.

For example, a baseline configured to evaluate every Sunday at 03:00 will, on its first run:

- Evaluate on Sunday between 03:00 and 05:00 on machines where the user was idle at 03:00.
- Evaluate up to 24 hours later (Monday) on machines where a user was actively signed in and using the device at 03:00.

All subsequent Sunday runs on both machines evaluate on Sunday within the 2-hour randomization window.

### Troubleshoot evaluation timing on the client

Use one of the following options to inspect what the client is doing with a scheduled baseline evaluation.

#### Find the schedule ID for your baseline deployment

The Configuration Manager client tracks each baseline **deployment** — not each baseline — using the deployment's **Assignment ID**. That same Assignment ID appears in `Scheduler.log` (prefixed with the schedule target) and in the client's WMI. Support Center also shows it as part of the deployment policy. Getting this ID is the first step to correlate console-side and client-side data.

To find the Assignment ID from the console:

1. In the Configuration Manager console, go to **Monitoring** > **Deployments**.
2. Filter the list by **Feature Type = Baseline** and locate your baseline deployment. If the **Deployment ID** column isn't shown, right-click the column header, choose **Column Settings**, and add it.
3. Copy the value from the **Deployment ID** column — this is the Assignment ID, a GUID similar to `{01234567-89AB-CDEF-0123-456789ABCDEF}`.

Alternatively, query the SMS Provider directly:

```powershell
Get-CMBaselineDeployment -Name "<baseline name>" |
    Select-Object AssignmentName, AssignmentUniqueID, TargetCollectionID
```

The `AssignmentUniqueID` value is what you'll look for on the client.

> [!NOTE]
> - In `Scheduler.log`, the Assignment ID is always prefixed with the schedule's target — `Machine/` for device-targeted deployments, or `<UserSID>/` for user-targeted deployments. For example, `Machine/{01234567-89AB-CDEF-0123-456789ABCDEF}`.
> - The client also creates auxiliary schedules for the same deployment with event prefixes on the ID itself — for example, `DEADLINE:<AssignmentUniqueID>` for the enforcement deadline. The base Assignment ID (no event prefix) is the main evaluation schedule; the event-prefixed variants govern related events.

#### Inspect `Scheduler.log`

Open `%WINDIR%\CCM\Logs\Scheduler.log` on the client. Each scheduled fire of a baseline evaluation is announced with an entry like the following, which contains both the internal trigger cookie and the schedule ID (the deployment's Assignment ID, prefixed with `Machine/` or the target user's SID):

```
SMSTrigger 'DA089D0000100008' for scheduler 'Machine/{01234567-89AB-CDEF-0123-456789ABCDEF}' will fire at 06/27/2026 05:10:00 PM with randomization.
```

See [Find the schedule ID for your baseline deployment](#find-the-schedule-id-for-your-baseline-deployment) above for how to obtain the GUID from the console. A two-pass search of `Scheduler.log` gives the complete picture:

1. **First pass — filter by the scheduler string** (for example `Machine/{01234567-89AB-CDEF-0123-456789ABCDEF}`) to see what happened to that specific deployment.
2. **Second pass — remove the filter** and look at the surrounding timeframe for global resource events (idle, power). These entries don't carry a schedule ID, so they won't appear in the filtered view.

**Per-schedule entries** (contain the schedule ID; visible in the filtered view):

| Entry | What it means |
|---|---|
| `SMSTrigger '<cookie>' for scheduler '<Machine\|SID>/<id>' will fire at <time> with randomization.` | The next scheduled fire time for this deployment, including the randomization window that will be applied. |
| `Schedule '<id>' with condition 0xa is putted into the pending queue.` | The launch conditions aren't currently met. `0xa` is the bitmask for **on-battery-above-low + idle**. |
| `>>> Adjusted deadline minutes from 1440 to <N> for schedule '<id>' because it was pending for a while.` | The client shortened the pending timer based on its history of the previous wait. On any recurring baseline of daily-or-longer cadence, `<N>` is `1`, which is why the second and later evaluations don't wait for the launch conditions. |
| `>>> Delay firing schedule '<id>'` | The launch conditions have been met (or the pending timer elapsed) and the evaluation is starting. |

**Global resource entries** (no schedule ID; view without a filter):

| Entry | What it means |
|---|---|
| `[Resource-Idle] Returning value 0.` | The client currently considers the device **not idle** (a user is present or otherwise active). |
| `[Resource-Idle] Returning value 1.` | The client currently considers the device **idle**. |
| `[Resource-Power] Raised event 'PowerStatus : <state>'` | The device's power state changed (AC / battery high / battery low / critical). |

If you see a first-run "putted into the pending queue" entry followed hours later by "Delay firing schedule" only after the timer elapsed, the device never went idle during the wait window — this is expected first-run behavior on a Windows client device with an active user.


> [!TIP]
> To evaluate a baseline immediately without waiting for the schedule or the launch conditions, open **Configuration Manager** in the Control Panel on the client, go to the **Configurations** tab, select the baseline, and click **Evaluate**. Results are cached for 15 minutes — see [Monitor compliance settings](monitor-compliance-settings.md#view-compliance-results-on-a-configuration-manager-windows-client-computer) for details.
