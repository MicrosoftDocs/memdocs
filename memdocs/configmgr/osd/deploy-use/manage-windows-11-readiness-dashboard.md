---
title: Manage Windows 11 readiness dashboard
titleSuffix: Configuration Manager
description: View the state of Windows 11 readiness dashboard using Configuration Manager
ms.date: 09/18/2023
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: article
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage Windows 11 readiness dashboard using Configuration Manager

*Applies to: Configuration Manager (current branch)*

In Configuration Manager, you can view the Windows 10 machines, which are ready for upgrade in your environment. Create collections for Windows 11 ready devices and deploy the upgrade. 

## Prerequisites

- For Configuration Manager version 2203 or later, the [WebView2 console extension](../../core/servers/manage/admin-console-extensions.md#bkmk_notification) must be installed. If needed, select the notification bell in the top right corner of the console to install the extension. <!--10024154-->

- Windows 10 telemetry services should be enabled at basic level
  
- Hardware inventory to be enabled on all client devices.

## <a name="bkmk_2309-dashboard"></a> Windows 11 upgrade readiness dashboard in version 2309 or later
<!--16875242-->
(*Introduced in version 2309*)

The Windows 11 upgrade readiness dashboard was created to make administrators or management aware of the devices, which are ready for upgrade. The following charts are displayed for the selected Collection:

**Windows Device Information** : Shows count of Windows 7, 8, 10 and 11 devices in your organization.

**Feature Update Version**: Shows count of each feature update Version in your organization.

**Upgrade Experience Indicators** : Shows information for each device, which can be in any of these states:

- Can't Upgrade (Red Color) devices to windows 11.
    
- App Upgrade/Uninstall required (Yellow Color) devices that need an application update or uninstall before upgrading to Windows 11.
    
- App/Driver upgrade required (Orange Color) devices that need application upgrade to windows 11.
    
- Ready for Upgrade (Green Color) devices that are capable of Windows 11 upgrade.
    
**Windows 11 Minimum Hardware Requirement** : Showcases the minimum hardware and software requirements needed to support Windows 11.

:::image type="content" source="media/17668425-windows11-dashboard.png" alt-text="Screenshot of Windows 11 readiness dashboard.":::

## Upgrade experience marker

The Upgrade Experience marker (UpgEx) is used more than any other appraiser marker. It provides a quick summary of the known compatibility issues that a device would encounter upon upgrade, boiling down to four colors:

   - **Red** : device can't be upgrade to the latest version of Windows. Attempts to run setup on a Red device results in a hard, impassable block (although if the device is red due to BDD, the customer sees a dismissive warning in setup).

   - **Orange** : device encounters regressions in functionality post-upgrade, including either an app that no longer runs or a device with no driver. Important note: none of the issues making a device Orange surface in setup.

   - **Yellow** : device needs to have an app uninstalled in order to upgrade. It is a major problem for the customer, but they're aware of the issue.

   - **Green** : none of the above issues are hit. Dismissive issues, like the Media Center or WMDRM warnings are Green. As a level-set, 95+% of devices are Green for 10-to-10 upgrades.

**Red**

The following conditions will all result in a device being marked Red:

- If the system fails any CPU requirement checks (SSE2, NX, CompareExchange128, LahfSahf, or PrefetchW). See the below section on CPU blocks for more.
- If the system has a BIOS block.
- If the system doesn’t have enough RAM. Requirement is 512 MB for Server, 1 GB for x86 Client, 2 GB for x64 Server, enforced with 10% wiggle room.
- If there’s a (non-network) device on the system that is considered boot critical and has its driver blocked.
- If there’s a wireless device that uses an XP-era emulated wireless driver.
- If a network device with an active connection loses its driver on upgrade (it means that the device would upgrade and lose access to WU).
- If the system has a block for which the enumerator is ComputerHardwareId, meaning we’ve dictated in the SDB that this specific model can’t upgrade.
- If there’s any other PNP device on the system that blocks upgrade not previously called out.
- If there’s a display-class device with a driver block that isn’t overridden AND no driver up level AND not already on BDD (customer would upgrade and have basic display).
- If the system reserve partition is < 15 MB, RedReason=SystemDriveFull (“We couldn’t update system reserved partition” error installing Windows 10 - Microsoft Support).

All except the last item will also hard block setup. The BDD block, however, can be bypassed by hitting the Dismiss button.

Starting with Windows 11, the UpgEx marker evaluates against the Windows 11 minimum hardware requirements. 

The following conditions will result in a device marked as Red for Windows 11:

- If a system doesn't support TPM 2.0 (RedReason=Tpm)
- If the system isn't Secure Boot Capable (RedReason=UefiSecureBoot)
- If the system has less than 4 GB of RAM (RedReason=Memory)
- If the system doesn't have 2 processor cores (RedReason=CPU)
- If the CPU doesn't support 1 ghz and higher speed (RedReason=CPU)
- If the CPU doesn't support the Windows 11 approved CPU generation (RedReason=CpuFms)
- If the system is in SMode and not a home (core) sku (RedReason=SModeState)
- If the system drive size is < 64 Gb (RedReason=SystemDriveSize)

**Orange** 

Orange is more complicated than Red. The following conditions trigger a machine to be Orange:

- If a non-system-class PNP device loses its driver on upgrade. Doesn't include display or active network, as those would make a device red.
- If any app or file will be blocked from running up level, isn't blocked downlevel, and doesn't get automatically removed. (Blocks take into account the UX_OVERRIDE declared in the SDB, which allows SDB authors to make an app block be considered benign for experience calculation).

The last bullet is tricky. Some examples:
- If app/file is blocked downlevel but also up level (such as an old app that's always been blocked): NOT orange
- If app/file is blocked only up level (such as a broken antivirus that gets removed): NOT orange
- If app/file is blocked only up level but has a UX_OVERRIDE of NO_BLOCK (such as an app that's not applicable post-upgrade): NOT orange
- If app/file isn't blocked up level at all: NOT orange

**Yellow**

Yellow status generally means that the customer needs to remove an app during setup.

Specifically, a machine is yellow in these cases:
- If any app has a soft block up level, taking into account UX_OVERRIDE (this won't surface in setup, but isn't severe enough to be Orange).

**Green**

Any device that doesn't meet the criteria for the other colors becomes Green. This includes devices that are warned about media center or WMDRM, and devices that have a problematic app removed silently during upgrade.


