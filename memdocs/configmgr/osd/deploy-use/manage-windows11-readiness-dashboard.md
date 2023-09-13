---
title: Manage Windows 11 readiness dashboard
titleSuffix: Configuration Manager
description: View the state of Windows 11 readiness dashboard using Configuration Manager
ms.date: 09/18/2023
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage Windows 11 readiness dashboard using Configuration Manager

*Applies to: Configuration Manager (current branch)*

In Configuration Manager, you can view the Windows 10 machines which are ready for upgrade in your environment. Create collections for Windows 11 ready devices and deploy the upgrade. 

## Prerequisites

- For Configuration Manager version 2203 or later, the [WebView2 console extension](../../core/servers/manage/admin-console-extensions.md#bkmk_notification) must be installed. If needed, select the notification bell in the top right corner of the console to install the extension. <!--10024154-->

- Windows 10 telemetry services should be enabled at basic level
  
- Hardware inventory to be enabled on all client devices.

## <a name="bkmk_2309-dashboard"></a> Windows 11 upgrade readiness dashboard in version 2309 or later
<!--16875242-->
(*Introduced in version 2309*)

The Windows 11 upgrade readiness dashboard was created to make administrators or management aware of the devices which are ready for upgrade. The following charts are displayed for the selected Collection:

**Windows Device Information** : Shows count of Windows 7, 8 , 10 and 11 devices in your organization.

**Feature Update Version**: Shows count of each feature update Version in your organization.

**Upgrade Experience Indicators** : Shows information for each device, which can be in any of these states:

- Cannot Upgrade (Red Color) devices that cannot be upgraded to windows 11.
    
- App Upgrade/Uninstall required (Yellow Color) devices that need an application update or uninstall before upgrading to Windows 11.
    
- App/Driver upgrade required (Orange Color) devices that need application upgrade to windows 11.
    
- Ready for Upgrade (Green Color) devices that are capable of Windows 11 upgrade.
    
**Windows 11 Minimum Hardware Requirement** : Showcases the minimum hardware and software requirements needed to support Windows 11.

:::image type="content" source="media/17668425-windows11-dashboard.png" alt-text="Windows 11 readiness dashboard.":::

## Upgrade experience marker

The Upgrade Experience marker (UpgEx) is used more than any other appraiser marker. It provides a quick summary of the known compatibility issues that a device would encounter upon upgrade, boiling down to four colors:

   - **Red** : device cannot upgrade to the latest version of Windows. Attempts to run setup on a Red device will generally result in a hard, impassable block (although if the device is red due to BDD, the customer will see a dismissible warning in setup).

   - **Orange** : device will encounter regressions in functionality post-upgrade, including either an app that no longer runs or a device with no driver. Important note: none of the issues that make a device Orange will be surfaced in setup.

   - **Yellow** : device will need to have an app uninstalled in order to upgrade. This may be a major problem for the customer, but at least they will be aware of the issue.

   - **Green** : none of the above issues will be hit. Note that dismissible issues, like the Media Center or WMDRM warnings will still be Green. As a level-set, 95+% of devices will be Green for 10-to-10 upgrades.

**Red**

The following conditions will all result in a device being marked Red:

- If the system fails any CPU requirement checks (SSE2, NX, CompareExchange128, LahfSahf, or PrefetchW). See the below section on CPU blocks for more.
- If the system has a BIOS block
- If the system doesn’t have enough RAM. Requirement is 512 MB for Server, 1 GB for x86 Client, 2 GB for x64 Server, enforced with 10% wiggle room
- If there’s a (non-network) device on the system that is considered boot critical and has its driver blocked
- If there’s a wireless device that uses an XP-era emulated wireless driver
- If a network device with an active connection will lose its driver on upgrade (in theory this means that the device would upgrade and lose access to WU)
- If the system has a block for which the enumerator is ComputerHardwareId, meaning we’ve dictated in the SDB that this specific model can’t upgrade
- If there’s any other PNP device on the system that blocks upgrade not already called out above
- If there’s a display-class device with a driver block that isn’t overridden AND no driver uplevel AND not already on BDD (customer would upgrade and have basic display)
- If the system reserve partition is < 15 MB, RedReason=SystemDriveFull (“We couldn’t update system reserved partition” error installing Windows 10 - Microsoft Support)

All except the last item will also hard block setup. The BDD block, however, can be bypassed by hitting the Dismiss button.

Starting with Windows 11, the UpgEx marker will also evaluate against the Windows 11 minimum hardware requirements. 

The following conditions will results in a device marked as Red for Windows 11:

- If a system does not support TPM 2.0 (RedReason=Tpm)
- If the system is not Secure Boot Capable (RedReason=UefiSecureBoot)
- If the system has less than 4 GB of RAM (RedReason=Memory)
- If the system is does not have 2 processor cores (RedReason=CPU)
- If the CPU does not support 1 ghz and higher speed (RedReason=CPU)
- If the CPU does not support the Windows 11 approved CPU generation (RedReason=CpuFms)
- If the system is in SMode and not a home (core) sku (RedReason=SModeState)
- If the system drive size is < 64 Gb (RedReason=SystemDriveSize)

**Orange** 

Orange is more complicated than Red. The following will trigger a machine to be Orange:

- If a non-system-class PNP device loses its driver on upgrade. Does not include display or active network, as those would make a device red.
- If any app or file will be blocked from running uplevel, is not blocked downlevel, and does not get automatically removed. (Blocks take into account the UX_OVERRIDE declared in the SDB, which allows SDB authors to make an app block be considered benign for experience calculation)

The last bullet is tricky. Some examples:
- If app/file is blocked downlevel but also uplevel (such as an old app that's always been blocked): NOT orange
- If app/file is blocked only uplevel but has a mig removal (such as a broken antivirus that gets removed): NOT orange
- If app/file is blocked only uplevel but has a UX_OVERRIDE of NO_BLOCK (such as an app that's just not applicable post-upgrade): NOT orange
- If app/file is not blocked uplevel at all: NOT orange

**Yellow**

Yellow status generally means that the customer will be required to remove an app during setup.

Specifically, a machine will be yellow in these cases:
- If any app has a softblock uplevel, taking into account UX_OVERRIDE (this will not surface in setup, but is not severe enough to be Orange)

**Green**

Any device that does not meet the criteria for the other colors becomes Green. This includes devices that will be warned about media center or WMDRM, as well as devices that will have a problematic app removed silently during upgrade.


