---
title: Windows quality update policy
description: Learn how to manage Windows quality updates in Microsoft Intune using quality updates policies, expedited updates, and Hotpatch to keep devices secure and compliant.
ms.date: 06/01/2026
ms.reviewer: Mounika
ms.topic: how-to
---

# Manage Windows quality updates

Windows quality updates are the regular Windows servicing updates that keep devices secure, reliable, and supported. These updates are released frequently—typically monthly—and include security fixes, non‑security improvements, and reliability enhancements. Because quality updates are cumulative, installing the latest update brings a device fully up to date for its currently installed Windows version.

In Microsoft Intune, Windows quality updates are managed through **quality updates policies**, which provide a dedicated policy surface for controlling how and when quality updates are delivered to devices. This policy is built on cloud‑based update orchestration and can be used alongside other Windows update policies, such as feature updates and driver updates. Depending on your deployment model, quality updates may be managed manually through Intune or automatically through Windows Autopatch. Client‑side update behavior—such as restart settings, deadlines, and notifications—continues to be controlled through standard Windows Update policy settings, including [update rings](update-rings.md) and [Windows Update client policies](/windows/deployment/update/waas-configure-wufb).

Quality updates policies also supports advanced deployment options for specific scenarios. You can **expedite updates** to fast‑track the installation of critical or security updates when waiting for regular deployment timelines isn't acceptable. For eligible Windows editions and device configurations, quality updates policies can also enable **Hotpatch**, which delivers certain security updates without requiring an immediate device restart. Together, these options help organizations balance rapid protection, deployment control, and user experience.

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

---

## Hotpatch updates

Windows quality updates policy allows you to deploy Hotpatch updates. Hotpatch updates are designed to reduce downtime and disruptions. Hotpatch updates are [Monthly B release security updates](/windows/deployment/update/release-cycle#monthly-security-update-release) that install and take effect without requiring you to restart the device. By minimizing the need to restart, these updates help ensure faster compliance, making it easier for organizations to maintain security while keeping workflows uninterrupted.

Hotpatch is an extension of Windows Update and requires Autopatch to create and deploy hotpatches to devices enrolled in the Autopatch quality update policy.

## Key benefits

- Hotpatch updates streamline the installation process and enhance compliance efficiency.
- No changes are required to your existing update ring configurations. Your existing ring configurations are honored alongside Hotpatch policies.
- The [Hotpatch quality update report](/windows/deployment/windows-autopatch/monitor/windows-autopatch-hotpatch-quality-update-report) provides a per policy level view of the current update statuses for all devices that receive Hotpatch updates.

## Prerequisites

[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]

To benefit from Hotpatch updates, devices must meet the following prerequisites:

- Windows 11 Enterprise version 24H2 or later
- Devices must be on the latest baseline release version to qualify for Hotpatch updates. Microsoft releases Baseline updates quarterly as standard cumulative updates. For more information on the latest schedule for these releases, see [Release notes for Hotpatch](https://support.microsoft.com/topic/release-notes-for-hotpatch-in-azure-automanage-for-windows-server-2022-4e234525-5bd5-4171-9886-b475dabe0ce8?preview=true).
- Microsoft Intune to manage hotpatch update deployment with the [Windows quality update policy with hotpatch turned on](#enroll-devices-to-receive-hotpatch-updates).

## Operating system configuration prerequisites

To prepare a device to receive Hotpatch updates, configure the following operating system settings on the device. You must configure these settings for the device to be offered the Hotpatch update and to apply all Hotpatch updates.

### Virtualization based security (VBS)

VBS must be turned on for a device to be offered Hotpatch updates. For information on how to set and detect if VBS is enabled, see [Virtualization-based Security (VBS)](/windows/security/hardware-security/enable-virtualization-based-protection-of-code-integrity?tabs=security).

> [!NOTE]
> Devices might be temporarily ineligible because they don't have VBS enabled or aren't currently on the latest baseline release. To ensure that all your Windows devices are configured properly to be eligible for hotpatch updates, see [Troubleshoot hotpatch updates](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates).

### Arm 64 devices must disable compiled hybrid PE usage (CHPE) (Arm 64 CPU Only)

> [!IMPORTANT]
> **Arm 64 device support is in public preview**.

To ensure all the Hotpatch updates are applied, you must set the **Compiled Hybrid Portable Executable** (CHPE) disable flag and restart the device to disable CHPE usage. You only need to set this flag one time. The registry setting remains applied through updates.

This requirement only applies to Arm 64 CPU devices when using Hotpatch updates. Hotpatch updates aren't compatible with servicing CHPE OS binaries.

To disable CHPE, create and/or set the following DWORD registry key:

Path: `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management DWORD key value: HotPatchRestrictions=1`

To learn more about CHPE, see [here](/windows/win32/winprog64/wow64-implementation-details)

> [!NOTE]
> There are no plans to support hotpatch updates on Arm64 devices with CHPE enabled. Disabling CHPE is required only for Arm64 devices. AMD and Intel CPUs don't have CHPE.

If you choose to no longer use Hotpatch updates, clear the CHPE disable flag (`HotPatchRestrictions=0`) then restart the device to turn on CHPE usage.

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

## Monitoring and reporting

After a Windows quality updates policy has been created with Hotpatch updates enabled, you can monitor results, hotpatch deployment status, and errors from the reports.

### Hotpatch quality updates

This report shows the total targeted devices and current update states of all Hotpatch update enabled devices.

1. Sign in to the Microsoft [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Reports > Windows quality updates** under **Windows Autopatch** section.

3. On the **Reports** tab, select **Hotpatch quality updates report**.

## Windows quality update distribution

This report shows the device distribution for different quality update releases. For Hotpatch applicable **Updates**, you can see both Hotpatch and standard quality update build numbers are displayed. Note that Hotpatch builds are lower numbered due to the inclusion of subset of fixes compared to standard builds. You can select **Devices on this update** column for each release to see a detailed list of devices and their corresponding updates.

To go to the device,

1. Sign in to the Microsoft [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select Reports > Windows updates.

3. On the Reports tab, click on Windows quality update distribution report.

Select **Update type** to select the quality update release. The **Build number** column on the Windows quality update distribution per feature version report shows you the Hotpatch and Standard builds.

