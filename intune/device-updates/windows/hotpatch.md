---
title: Hotpatch updates with Windows quality updates policies
description: Learn about Windows Hotpatch updates and how to manage them with Microsoft Intune quality updates policies.
ms.date: 01/06/2026
ms.reviewer: Mounika
ms.topic: how-to
---

# Hotpatch updates

Windows quality updates policy allows you to deploy Hotpatch updates. Hotpatch updates are designed to reduce downtime and disruptions. Hotpatch updates are [Monthly B release security updates](/windows/deployment/update/release-cycle#monthly-security-update-release) that install and take effect without requiring you to restart the device. By minimizing the need to restart, these updates help ensure faster compliance, making it easier for organizations to maintain security while keeping workflows uninterrupted.

Hotpatch is an extension of Windows Update and requires Autopatch to create and deploy hotpatches to devices enrolled in the Autopatch quality update policy.

## Key benefits

- Hotpatch updates streamline the installation process and enhance compliance efficiency.
- No changes are required to your existing update ring configurations. Your existing ring configurations are honored alongside Hotpatch policies.
- The [Hotpatch quality update report](/windows/deployment/windows-autopatch/monitor/windows-autopatch-hotpatch-quality-update-report) provides a per policy level view of the current update statuses for all devices that receive Hotpatch updates.

## Prerequisites

Hotpatch updates have the same [prerequisites](quality-updates.md#prerequisites) as quality updates policies. This section highlights additional prerequisites specific to Hotpatch updates.

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> To prepare a device to receive Hotpatch updates, configure the following operating system settings on the device. You must configure these settings for the device to be offered the Hotpatch update and to apply all Hotpatch updates.
> ### Virtualization based security (VBS)
>VBS must be turned on for a device to be offered Hotpatch updates. For information on how to set and detect if VBS is enabled, see [Virtualization-based Security (VBS)](/windows/security/hardware-security/enable-virtualization-based-protection-of-code-integrity?tabs=security).
>
>> [!NOTE]
>> Devices might be temporarily ineligible because they don't have VBS enabled or aren't currently on the latest baseline release. To ensure that all your Windows devices are configured properly to be eligible for hotpatch updates, see [Troubleshoot hotpatch updates](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates).
>
> ### Arm 64 devices must disable compiled hybrid PE usage (CHPE) (Arm 64 CPU Only> )
>
> > [!IMPORTANT]
> > **Arm 64 device support is in public preview**> .
>
> To ensure all the Hotpatch updates are applied, you must set the **Compiled Hybrid Portable Executable** (CHPE) disable flag and restart the device to disable CHPE > usage. You only need to set this flag one time. The registry setting remains applied through updates> .
>
> This requirement only applies to Arm 64 CPU devices when using Hotpatch updates. Hotpatch updates aren't compatible with servicing CHPE OS binaries> .
>
> To disable CHPE, create and/or set the following DWORD registry key> :
>
> Path: `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management DWORD key value: HotPatchRestrictions=1> `
>
> To learn more about CHPE, see [here](/windows/win32/winprog64/wow64-implementation-details> )
>
> > [!NOTE]
> > There are no plans to support hotpatch updates on Arm64 devices with CHPE enabled. Disabling CHPE is required only for Arm64 devices. AMD and Intel CPUs don't have > CHPE.
> If you choose to no longer use Hotpatch updates, clear the CHPE disable flag (`HotPatchRestrictions=0`) then restart the device to turn on CHPE usage.
:::column-end:::
:::row-end:::


## Ineligible devices

Devices that don't meet one or more prerequisites automatically receive the Latest Cumulative Update (LCU) instead. Latest Cumulative Update (LCU) contains monthly updates that supersede the previous month's updates containing both security and nonsecurity releases.

LCUs requires you to restart the device, but the LCU ensures that the device remains fully secure and compliant.

> [!NOTE]
> If devices aren't eligible for Hotpatch updates, these devices are offered the LCU. The LCU keeps your configured Update ring settings, it doesn't change the settings.

## Release cycles

For more information about the release calendar for hotpatch updates, see [Release notes for Hotpatch](https://support.microsoft.com/topic/release-notes-for-hotpatch-public-preview-on-windows-11-version-24h2-enterprise-clients-c117ee02-fd35-4612-8ea9-949c5d0ba6d1).

- Baseline: Includes the latest security fixes, cumulative new features, and enhancements. Restart required.
- Hotpatch: Includes security updates. No restarted required.

| Quarter | Baseline updates (requires restart) | Hotpatch (no restart required) |
| ----- | ----- | ----- |
| 1 | January | February and March |
| 2 | April | May and June |
| 3 | July | August and September |
| 4 | October | November and December |

## Hotpatch on Windows 11 Enterprise or Windows Server 2025

> [!NOTE]
> Hotpatch is also available on Windows Server and Windows 365. For more information, see [Hotpatch for Windows Server Azure Edition](/windows-server/get-started/enable-hotpatch-azure-edition).

Hotpatch updates are similar between Windows 11 and Windows Server 2025.

- Windows Autopatch manages Windows 11 updates
- Azure Update Manager and optional Azure Arc subscription for Windows 2025 Datacenter/Standard Editions (on-premises) manages Windows Server 2025 Datacenter Azure Edition. For more information, on Windows Server and Windows 365, see [Hotpatch for Windows Server Azure Edition](/windows-server/get-started/enable-hotpatch-azure-edition).

The calendar dates, eight hotpatch months, and four baseline months, planned each year are the same for all the hotpatch-supported operating systems (OS). It's possible for additional baseline months for one OS (for example, Windows Server 2022), while there are hotpatch months for another OS, such as Server 2025 or Windows 11, version 24H2. Review the release notes from [Windows release health](/windows/release-health/) to keep up to date.

## Enroll devices to receive Hotpatch updates

> [!NOTE]
> If you're using Autopatch groups and want your devices to receive Hotpatch updates, you must create a Hotpatch policy and assign devices to it. Turning on Hotpatch updates doesn't change the deferral setting applied to devices within an Autopatch group.

**To enroll devices to receive Hotpatch updates:**

1. Go to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** from the left navigation menu.
1. Under the **Manage updates** section, select **Windows updates**.
1. Go to the **Quality updates** tab.
1. Select **Create**, and select **Windows quality update policy**.
1. Under the **Basics** section, enter a name for your new policy and select Next.
1. Under the **Settings** section, set **"When available, apply without restarting the device ("Hotpatch")** to **Allow**. Then, select **Next**.
1. Select the appropriate Scope tags or leave as Default. Then, select **Next**.
1. Assign the devices to the policy and select **Next**.
1. Review the policy and select **Create**.

These steps ensure that targeted devices, which are [eligible](#prerequisites) to receive Hotpatch updates, are configured properly. [Ineligible devices](#ineligible-devices) are offered the latest cumulative updates (LCU).

> [!NOTE]
> Turning on Hotpatch updates doesn't change the existing deadline-driven or scheduled install configurations on your managed devices. Deferral and active hour settings still apply.

## Roll back a hotpatch update

Automatic rollback of a Hotpatch update isn't supported but you can uninstall them. If you experience an unexpected issue with hotpatch updates, you can investigate by uninstalling the hotpatch update and installing the latest standard cumulative update (LCU) and restart. Uninstalling a hotpatch update is quick, however, it does require a device restart.
