---
title: Startup performance in Endpoint Analytics
titleSuffix: Microsoft Intune
description: Get details about device startup performance in Endpoint Analytics
ms.date: 10/23/2023
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: conceptual
author: smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---

# <a name="bkmk_bp"></a> Startup performance

The startup performance score helps IT get users from power-on to productivity quickly, without lengthy boot and sign-in delays.

## <a name="bkmk_prereq"></a> Prerequisites

For devices enrolled via Intune, Startup performance insights are only available for:

- Devices running an Enterprise, Professional, or Education edition of Windows 10 version 1903 or later.
  - Windows 10 Pro versions 1903 and 1909 require [KB4577062](https://support.microsoft.com/help/4577062/windows-10-update-kb4577062). <!--8392089, 8389021-->
  - Windows 10 Pro versions 2004 and 20H2 require [KB4577063](https://support.microsoft.com/help/4577063/windows-10-update-kb4577063). <!--8392089, 8389021-->
  - Long-term servicing channel (LTSC) and Home editions aren't currently supported.
- The devices must be Microsoft Entra joined or Microsoft Entra hybrid joined.
  - Workplace joined machines aren't currently supported.

For devices that don't meet the above criteria, you're able to [enroll via Configuration Manager](enroll-configmgr.md).

> [!IMPORTANT]
> Client devices require a restart to fully enable all analytics. <!--7698085--> The retention period for device boot and sign-in events is 29 days. If a device has not uploaded a boot or sign-in event in the past 29 days, it will not appear in the Startup performance report.

## <a name="bkmk_score"></a> Startup score

[!INCLUDE [Endpoint analytics startup score](includes/startup-score.md)]

[![Endpoint analytics startup performance page](media/startup-performance.png)](media/startup-performance.png#lightbox)

> [!NOTE]
> If you are not seeing startup performance data from all your devices, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

## Insights

The **Startup performance** page also provides a prioritized list of **Insights and recommendations**, described in the following sections:

### <a name="bkmk_hdd"></a> Hard disk drives

Startup performance provides an insight on the number of devices on which the boot drive is a hard disk. Hard disk drives typically result in boot times three to four times longer than solid-state drives. We also report the expected improvement to start up performance you would gain by moving to solid-state drives.

Scroll through to see the list of devices that have hard disk drives. The recommended action is to upgrade these devices to solid-state drives.

### <a name="bkmk_gp"></a> Group Policy

Startup performance provides an insight on the number of devices that have delays to boot and sign-in times caused by Group Policy. Clicking through takes you to the devices view. The view is sorted by Group Policy time, so you can see affected devices for further troubleshooting.

Select a particular device, to see its boot and sign-in history. The history helps you determine if the issue is a regression and when it might have occurred.

While there are many articles on how to optimize Group Policies performance, you might choose to migrate to cloud-management instead. Migrating to cloud-management allows you to use [Intune security baselines](../intune/protect/security-baselines.md) and [Group Policy analytics](../intune/configuration/group-policy-analytics.md).

### <a name="bkmk_sb"></a> Slow boot and sign-in times

Startup performance provides an insight on the number of devices with slow boot or sign-in times. A boot score or sign-in score of "0" means it's slow. Clicking through takes you to the devices view. The devices are sorted by core boot time or core sign-in time respectively, so you can see affected devices for further troubleshooting.

Select a particular device, to see its boot and sign-in history. The history helps you determine if the issue was a regression and when it might have occurred.

## <a name="bkmk_report"></a> Reporting tabs

The **Startup performance** page has reporting tabs that provide support for the insights, including:

- **Model performance**. This tab lets you see the boot and sign-in performance by device model, which can help you identify if performance problems are isolated to particular models.
- **Device performance**. This tab provides boot and sign-in metrics for all your devices. You can sort by a particular metric (for example, GP sign-in time) to see which devices have the worst scores for that metric to help with troubleshooting. You can also search for a device by name. Select a device to see its boot and sign-in history, which can help you identify if there was a recent regression
  > [!Note]
  > In the **Device performance** tabs of Endpoint analytics, admins will only see devices they have access to according to their assigned Scope tags. To learn more about Scope tags, see [Scope tags for distributed IT](../intune/fundamentals/scope-tags.md). Aggregated insights, such as scores and summary views are calculated using all enrolled devices in the tenant. To apply Scope tags to aggregated insights, see [Device scopes in Endpoint analytics](device-scopes.md).

- **Startup processes**. Startup processes can negatively affect user experience by increasing the length of time that users must wait for the desktop to become responsive. This tab shows you which processes are impacting the sign-in "time to responsive desktop" phase and keeps the CPU above 50% after the desktop has rendered. The table only lists processes that affect a minimum of 10 devices in your tenant. When you review the startup processes, the following data calculations are displayed:
  - **Device count**: The count of devices that experienced a delay to a responsive desktop from the process.
  - **Median delay**: The median delay time of the process for the counted devices.
  - **Total delay**: The sum of the delays for all of the counted devices.

## Known issues

[!INCLUDE [Endpoint analytics export to csv value mapping known issue](includes/known-issue-csv-mapping.md)]

## Next steps

- Use the [Work from anywhere report](work-from-anywhere.md).
- Use [Remediations](../intune/fundamentals/remediations.md) to help fix common support issues before end-users notice issues.
