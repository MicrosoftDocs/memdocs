---
title: Power Management Views
titleSuffix: Configuration Manager
description: Information about the power plans applied to computers by Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: bfb0f6a9-09c1-4065-b0e5-be06cdc1800a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Power Management Views in Configuration Manager

Information about the power plans applied to computers by Configuration Manager and the power capabilities of computers is retrieved by Configuration Manager hardware inventory.

For more information about power management, see [Power Management in Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/gg682043(v=technet.10)).

Wake up proxy is used to supplement the traditional wake-up packet method by using the wake-up proxy client settings. Wake-up proxy uses a peer-to-peer protocol and elected computers to check whether other computers on the subnet are awake, and to wake them if necessary.

For more information about wake up proxy, see the Power Management section of the [About Client Settings in Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/gg682067(v=technet.10)) topic in the Configuration Manager Documentation Library.

## Power Management Views

The power management views are described in this section.

### v_GS_POWER_MANAGEMENT_CAPABILITIES

Lists information about the power management capabilities collected from each client computer, sorted by resource ID, including information about the last time this information was collected, information about the battery, if present, and information about the wake up capabilities of the computer.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_POWER_MANAGEMENT_CLIENTOPTOUT_SETTINGS

Lists information for each client computer about whether the administrator allows the computer to opt out from power management settings and whether the client computer has been opted out from the settings. This view is sorted by resource ID.

### v_GS_POWER_MANAGEMENT_CONFIGURATION

Lists information about power plan names and the duration of each power plan that have been applied to client computers.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_POWER_MANAGEMENT_DAY

Lists information about power activity on computers for each hour of the day.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_POWER_MANAGEMENT_MONTH

List information about power activity on computers for the previous month, such as when the computer was active, when it was turned on, and when it was inn sleep mode.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_POWER_MANAGEMENT_SETTINGS

Lists information about the power management settings applied to each computer, sorted by resource ID. These settings include the power plan applied to the computer, the delay before the screen and hard disks are turned off, and the action that will be taken when the computer power button is pressed.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_POWER_MANAGEMENT_SUSPEND_ERROR

Lists information, by Resource ID, about power management suspend operations that did not complete successfully.
The view can be joined to other views by using the **ResourceID** column.

## Wake Up Proxy Views

The wake up proxy views are described in this section.

### v_WakeupProxyDeploymentState

Lists information about the computers in each collection and whether that computer is enabled for wake-up proxy. This view is sorted by collection ID.
This view can be joined to other views by using the **CollectionID** column.

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md) 