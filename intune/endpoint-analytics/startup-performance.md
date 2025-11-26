---
title: Startup Performance in Endpoint Analytics
description: Learn how startup performance in Microsoft Intune endpoint analytics helps analyze boot times, identify issues, and optimize device performance.
ms.date: 10/09/2025
ms.topic: concept-article
---

# Startup performance

The **Startup performance** page in endpoint analytics provides insights into the startup performance of your Windows devices. It helps you identify and remediate issues that can lead to slow boot and sign-in times.

> [!IMPORTANT]
> Clients require a restart to fully enable all analytics. <!--7698085--> The retention period for device boot and sign-in events is 29 days. If a device hasn't uploaded a boot or sign-in event in the past 29 days, it does not appear in the Startup performance report.

## Startup score

The **startup score** helps IT get users from power-on to productivity quickly, without lengthy boot and sign-in delays. The **Startup score** is a number between 0 and 100. This score is a weighted average of **Boot score** and the **Sign-in** score, which are computed as follows:

- **Boot score**: Based on the time from power-on to sign in. We look at the last boot time from each device, excluding the update phase, then score it from 0 (poor) to 100 (exceptional). These scores are averaged to provide an overall tenant boot score.
- **Sign-in score**: Based on the time from when credentials have been entered until the user can access a responsive desktop (meaning the desktop has rendered and the CPU usage has fallen below a moderate level or the device responds to an action initiated by the user). We look at the last sign-in time to each device, excluding first sign-ins or sign-ins immediately after a feature update, then score it from 0 (poor) to 100 (exceptional). These scores are averaged to provide an overall tenant boot score.

[![Endpoint analytics startup performance page](images/startup-performance.png)](images/startup-performance.png#lightbox)

> [!NOTE]
> If you aren't seeing startup performance data from all your devices, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#troubleshooting-device-enrollment-and-startup-performance).

## Insights

The **Startup performance** page also provides a prioritized list of **Insights and recommendations**, described in the following sections:

### Hard disk drives

Startup performance provides an insight on the number of devices on which the boot drive is a hard disk. Hard disk drives typically result in boot times three to four times longer than solid-state drives. We also report the expected improvement to start up performance you would gain by moving to solid-state drives.

Scroll through to see the list of devices that have hard disk drives. The recommended action is to upgrade these devices to solid-state drives.

### Group Policy

Startup performance provides an insight on the number of devices that have delays to boot and sign-in times caused by Group Policy. Clicking through takes you to the devices view. The view is sorted by Group Policy time, so you can see affected devices for further troubleshooting.

Select a particular device, to see its boot and sign-in history. The history helps you determine if the issue is a regression and when it might have occurred.

While there are many articles on how to optimize Group Policies performance, you might choose to migrate to cloud-management instead. Migrating to cloud-management allows you to use [Intune security baselines](../intune-service/protect/security-baselines.md) and [Group Policy analytics](../intune-service/configuration/group-policy-analytics.md).

### Slow boot and sign-in times

Startup performance provides an insight on the number of devices with slow boot or sign-in times. A boot score or sign-in score of "0" means it's slow. Clicking through takes you to the devices view. The devices are sorted by core boot time or core sign-in time respectively, so you can see affected devices for further troubleshooting.

Select a particular device, to see its boot and sign-in history. The history helps you determine if the issue was a regression and when it occurred.

## Reporting tabs

The **Startup performance** page has reporting tabs that provide support for the insights, including:

- **Model performance**. This tab lets you see the boot and sign-in performance by device model, which can help you identify if performance problems are isolated to particular models.
- **Device performance**. This tab provides boot and sign-in metrics for all your devices. You can sort by a particular metric (for example, GP sign-in time) to see which devices have the worst scores for that metric to help with troubleshooting. You can also search for a device by name. Select a device to see its boot and sign-in history, which can help you identify if there was a recent regression
  > [!Note]
  > In the **Device performance** tabs of endpoint analytics, admins will only see devices they have access to according to their assigned Scope tags. To learn more about Scope tags, see [Scope tags for distributed IT](../intune-service/fundamentals/scope-tags.md). Aggregated insights, such as scores and summary views are calculated using all enrolled devices in the tenant. To apply Scope tags to aggregated insights, see [Device scopes in endpoint analytics](../advanced-analytics/device-scopes.md).

- **Startup processes**. Startup processes can negatively affect user experience by increasing the length of time that users must wait for the desktop to become responsive. This tab shows you which processes are impacting the sign-in "time to responsive desktop" phase and keeps the CPU above 50% after the desktop is rendered. The table only lists processes that affect a minimum of 10 devices in your tenant. When you review the startup processes, the following data calculations are displayed:
  - **Device count**: The count of devices that experienced a delay to a responsive desktop from the process.
  - **Median delay**: The median delay time of the process for the counted devices.
  - **Total delay**: The sum of the delays for all of the counted devices.

## Related content

- Understand [endpoint analytics scores, baselines, and insights](scores.md)
- Use the [application reliability report](app-reliability.md) to identify apps that are causing crashes or hangs during startup.
- Use the [Startup performance score](tartup-performance) to understand how startup performance affects your overall endpoint analytics score.
- Use the [Work from anywhere report](work-from-anywhere.md).
- Use [Remediations](../intune-service/fundamentals/remediations.md) to help fix common support issues before end-users notice issues.
