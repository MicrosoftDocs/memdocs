---
title: Use Hotpatch With Windows Quality Updates
description: Learn how hotpatch works with Windows quality update policies in Microsoft Intune to install eligible security updates without requiring an immediate device restart.
ms.date: 01/13/2026
ms.reviewer: mobattul
ms.topic: how-to
---

# Hotpatch for Windows quality updates

With hotpatch updates, you can quickly take measures to help protect your organization from the evolving landscape of cyberattacks, while minimizing user disruptions. Hotpatch updates are *Monthly B release* security updates that install and take effect without requiring you to restart the device. By minimizing the need to restart, these updates help ensure faster compliance, making it easier for organizations to maintain security while keeping workflows uninterrupted. 

Hotpatch security updates are enabled by default for all eligible devices in Microsoft Intune. This approach helps organizations maintain security compliance while minimizing workflow interruptions.  

You can configure if hotpatch is enabled for you devices using either a tenant level setting or quality update policies.  

### Key benefits

- **Faster security**: Hotpatch security fixes take effect without requiring a restart, getting devices secure much more quickly.  
- **Reduced disruption**: Hotpatch installs eligible security updates without requiring an immediate device restart, helping users stay productive.
- **Smaller payloads**: Hotpatch package size is significantly smaller than the standard cumulative updates. 
- **No changes to existing update rings**: Existing update ring configurations remain in effect and are honored alongside hotpatch configurations.
- **Policy‑level visibility**: The hotpatch quality updates report provides a policy‑level view of update status for devices receiving hotpatch updates.

## Prerequisites

Hotpatch has the same [prerequisites](quality-updates.md#prerequisites) as Windows quality update policies. This section highlights additional prerequisites specific to hotpatch.

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> To prepare a device to receive hotpatch updates, configure the following operating system settings on the device. You must configure these settings for the device to be offered the hotpatch update and to apply all hotpatch updates.
>
>**Virtualization based security (VBS)**\
>VBS must be turned on for a device to be offered hotpatch updates. For information on how to set and detect if VBS is enabled, see [Virtualization-based Security (VBS)](/windows/security/hardware-security/enable-virtualization-based-protection-of-code-integrity?tabs=security).
>
>> [!NOTE]
>> Devices might be temporarily ineligible because they don't have VBS enabled or aren't currently on the latest baseline release. To ensure that all your Windows devices are configured properly to be eligible for hotpatch updates, see [Troubleshoot hotpatch updates](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates).
>
> You can also find VBS status in [Autopatch alerts and remediation](/windows/deployment/windows-autopatch/monitor/alerts-remediations) with the alert *Hotpatch - VBS not running*. 
>
>**Arm 64 devices must disable compiled hybrid PE usage (CHPE) (Arm 64 CPU Only)**
>
> To ensure all the hotpatch updates are applied, you must set the **Compiled Hybrid Portable Executable** (CHPE) disable flag and restart the device to disable CHPE usage. You only need to set this flag one time. The registry setting remains applied through updates.
>
> This requirement only applies to Arm 64 CPU devices when using hotpatch updates. Hotpatch updates aren't compatible with servicing CHPE OS binaries.
>
> To disable CHPE, create and/or set the following DWORD registry key:
>
> Path: `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management DWORD key value: HotPatchRestrictions=1`
>
> To learn more about CHPE, see [here](/windows/win32/winprog64/wow64-implementation-details)
>
> > [!NOTE]
> > There are no plans to support hotpatch updates on Arm64 devices with CHPE enabled. Disabling CHPE is required only for Arm64 devices. AMD and Intel CPUs don't have CHPE.
> If you choose to no longer use hotpatch updates, clear the CHPE disable flag (`HotPatchRestrictions=0`) then restart the device to turn on CHPE usage.
:::column-end:::
:::row-end:::

### Ineligible devices

Devices that don't meet one or more prerequisites automatically receive the Latest Cumulative Update (LCU) instead. Latest Cumulative Update (LCU) contains monthly updates that supersede the previous month's updates containing both security and nonsecurity releases.

LCUs requires you to restart the device, but the LCU ensures that the device remains fully secure and compliant.

> [!NOTE]
> If devices aren't eligible for hotpatch updates, these devices are offered the LCU. The LCU keeps your configured Update ring settings, it doesn't change the settings.

## Release cycles

For more information about the release calendar for hotpatch updates, see [Release notes for hotpatch](https://support.microsoft.com/topic/release-notes-for-hotpatch-public-preview-on-windows-11-version-24h2-enterprise-clients-c117ee02-fd35-4612-8ea9-949c5d0ba6d1).

- Baseline: Includes the latest security fixes, cumulative new features, and enhancements. Restart required.
- Hotpatch: Includes security updates. No restarted required.

| Quarter | Baseline updates (requires restart) | Hotpatch (no restart required) |
| ----- | ----- | ----- |
| 1 | January | February and March |
| 2 | April | May and June |
| 3 | July | August and September |
| 4 | October | November and December |

During a hotpatch month, if a device has hotpatch updates enabled but isn't on the latest baseline update, the device will receive both the latest baseline update (restart required) and the latest hotpatch update.

> [!NOTE]
> Upgrading a hotpatch enrolled device to the latest Windows version (e.g. upgrading from Windows 11, version 24H2 to Windows 11, version 25H2) during a baseline month keeps the device on the hotpatch cycle, and the device keeps receiving the hotpatch updates seamlessly. However, upgrading a device to the latest Windows version in a hotpatch month switches the device to standard updates; you must restart the device to apply the update until the next baseline release. 

## Hotpatch on Windows 11 Enterprise or Windows Server 2025

> [!NOTE]
> Hotpatch is also available on Windows Server and Windows 365. For more information, see [Hotpatch for Windows Server Azure Edition](/windows-server/get-started/enable-hotpatch-azure-edition).

Hotpatch updates are similar between Windows 11 and Windows Server 2025.

- Windows Autopatch manages Windows 11 updates
- Azure Update Manager and optional Azure Arc subscription for Windows 2025 Datacenter/Standard Editions (on-premises) manages Windows Server 2025 Datacenter Azure Edition.

The calendar dates, eight hotpatch months, and four baseline months, planned each year are the same for all the hotpatch-supported operating systems. It's possible for additional baseline months for one OS (for example, Windows Server 2022), while there are hotpatch months for another OS, such as Server 2025 or Windows 11, version 24H2. Review the release notes from [Windows release health](/windows/release-health/) to keep up to date.

## Enroll devices to receive hotpatch updates

You can enable hotpatch updates for your devices using a tenant level setting or quality update policies. The tenant level setting is the default setting applied to devices that aren't members of a quality update policy. If a device is assigned to a quality update policy, the hotpatch setting from that policy is the one applied.

### Default hotpatch tenant setting 

The default tenant setting is only applied to devices that aren't members of a quality update policy.

Windows Autopatch respects your configuration of quality update policies. If a device is assigned to one of those policies, the hotpatch setting from that policy is the one applied.  

Configure the default hotpatch update behavior for your tenant as follows:

1. In the [Microsoft Intune admin center][INT-AC], select **Tenant administration** > **Windows Autopatch** > **Tenant management**. 
1. Select the **Tenant settings** tab. 
1. Toggle the **When available, apply updates without restarting the device ("hotpatch")** setting to either **Allow** or **Block**.

### Configure hotpatch using quality update policies.

Windows Autopatch respects your configuration of the hotpatch setting in quality update policies. If a device is assigned to one of those policies, the hotpatch setting from that policy is the one applied, not the tenant default setting.  

To enroll devices to receive hotpatch updates:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows updates**.
1. Select the **Quality updates** tab.
1. Select **Create**, and select **Windows quality update policy**.
1. Under the **Basics** section, enter a name for your new policy and select **Next**.
1. Under the **Settings** section, set **When available, apply without restarting the device ("hotpatch")** to **Allow**. Then, select **Next**.
1. Select the appropriate Scope tags or leave as Default. Then, select **Next**.
1. Assign the devices to the policy and select **Next**.
1. Review the policy and select **Create**.

These steps ensure that targeted devices, which are [eligible](#prerequisites) to receive hotpatch updates, are configured properly. [Ineligible devices](#ineligible-devices) are offered the latest cumulative updates (LCU).

> [!NOTE]
> Turning on hotpatch updates doesn't change the existing deadline-driven or scheduled install configurations on your managed devices. Deferral and active hour settings still apply.

## Roll back a hotpatch update

Automatic rollback of a hotpatch update isn't supported but you can uninstall them. If you experience an unexpected issue with hotpatch updates, you can investigate by uninstalling the hotpatch update and installing the latest standard cumulative update (LCU) and restart. Uninstalling a hotpatch update is quick, however, it requires a device restart.

## Hotpatch quality updates report

After a Windows quality update policy has been created with hotpatch updates enabled, you can monitor results, hotpatch deployment status, and errors from the reports.

This report shows the total targeted devices and current update states of all hotpatch update enabled devices.

To access the report:

1. In the [Microsoft Intune admin center][INT-AC], select **Reports**
1. Under the **Windows Autopatch** section, select **Windows quality updates**
1. On the **Reports** tab, select **Hotpatch quality updates report**.

## Troubleshoot hotpatch updates

### Step 1: Verify the device is eligible for hotpatch updates and on a hotpatch baseline before the hotpatch update is installed 

Hotpatching follows the hotpatch release cycle. Review the prerequisites to ensure the device is eligible for hotpatch updates. For information on devices that don't meet the prerequisites, see [Ineligible devices](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates#ineligible-devices). 

For the latest release schedule, see the [hotpatch release notes](https://support.microsoft.com/topic/release-notes-for-hotpatch-public-preview-on-windows-11-version-24h2-enterprise-clients-c117ee02-fd35-4612-8ea9-949c5d0ba6d1). For information on Windows update history, see [Windows 11, version 24H2 update history](https://support.microsoft.com/topic/windows-11-version-24h2-update-history-0929c747-1815-4543-8461-0160d16f15e5). 

### Step 2: Verify the device has Virtualization-based security (VBS) turned on 

1. Select Start, and enter *System information* in the Search. 
1. Select **System information** from the results. 
1. Under **System summary**, under the Item column, find **Virtualization-based security**. 
1. Under the **Value** column, ensure it states *Running*. 

### Step 3: Verify the device is properly configured to turn on hotpatch updates 

1. In Intune, review your configured policies within Windows Autopatch to see which groups of devices are targeted with a hotpatch policy by going to the **Windows Update** > **Quality Updates** page. 
1. Ensure the hotpatch update policy is set to **Allow**. 
1. On the device, select **Start** > **Settings** > **Windows Update** > **Advanced options** > **Configured update policies** > find **Enable hotpatching when available**. This setting indicates that the device is enrolled in hotpatch updates as configured by Windows Autopatch. 

### Step 4: Disable compiled hybrid PE usage (CHPE) (Arm64 CPU only) 

For more information, see [Arm 64 devices must disable compiled hybrid PE usage (CHPE) (Arm 64 CPU Only)](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates). 

### Step 5: Use Event viewer to verify the device has hotpatch updates turned on 

1. Right-click on the Start menu, and select **Event viewer**. 
1. Search for *AllowRebootlessUpdates* in the filter. If *AllowRebootlessUpdates* is set to `1`, the device is enrolled in the Autopatch update policy and has hotpatch updates turned on:
    `"data": { "payload": "{\"Orchestrator\":{\"UpdatePolicy\":{\"Update/AllowRebootlessUpdates\":true}}}", "isEnrolled": 1, "isCached": 1, "vbsState": 2,`

### Step 6: Check Windows Logs for any hotpatch errors 

Hotpatch updates provide an inbox monitor service that checks for the health of the updates installed on the device. If the monitor service detects an error, the service logs an event in the Windows Application Logs. If there's a critical error, the device installs the standard (LCU) update to ensure the device is fully secure. 

1. Right-click on the Start menu, and select **Event viewer**. 
1. Search for *hotpatch* in the filter to view the logs. 

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431