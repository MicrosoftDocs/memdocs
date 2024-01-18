---
title: Create and apply power plans
titleSuffix: Configuration Manager
description: Create and apply power plans in Configuration Manager.
ms.date: 10/12/2020
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to create and apply power plans in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Power management in Configuration Manager enables you to apply power plans to collections of computers in your hierarchy. Configuration Manager defines several power plans, or you can create your own custom power plans.

You can only apply Configuration Manager power plans to device collections. If a computer is a member of multiple collections, each with different power plans, then the following actions happen:

- Power plan: If policy applies multiple values for power settings on a computer, it uses the least restrictive value.

- Wakeup time: If policy applies multiple wakeup times to a desktop computer, it uses the time closest to midnight.

To display all computers that have multiple power plans applied to them, use the **Computers with Multiple Power Plans** report. This report can help you discover computers that have power conflicts. For more information about power management reports, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).

Make sure to review any power settings that you apply from group policy. Power settings configured by using group policy will override settings configured by Configuration Manager power management.

> [!IMPORTANT]
> Systems that you enable for **Modern Standby** (S0) won't apply Configuration Manager power policies. You'll see a message similar to the following in the PwrProvider.log: `The "Required idleness to sleep" setting (<738eddaa-52e2-467f-b453-821ef2884d47>) is not supported on this operating system. This setting will be ignored.`<!-- SCCMDocs#2177 -->

## Create and apply a power plan

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.

1. In the **Assets and Compliance** workspace, select the **Device Collections** node.

1. In the **Device Collections** list, choose the collection to which you want to apply power management settings. In the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Power Management** tab of the collection, and select **Specify power management settings for this collection**.

    > [!NOTE]
    > You can also select **Browse**, and copy the power management settings from another collection to this collection.

1. Specify the **Start** and **End** time for peak (or business) hours.

1. To specify a time when a desktop computer wakes from sleep or hibernate, Enable **Wakeup time (desktop computers)**. When the client wakes up, it can install scheduled software updates or other deployments.

    > [!IMPORTANT]
    > Power management uses the internal Windows wakeup time feature to wake computers from sleep or hibernate. Wakeup time settings aren't applied to portable computers to prevent scenarios in which they might wake when not plugged in. The wake up time is randomized and computers will be woken over a one hour period from the specified wakeup time.

1. If you want to configure a custom power plan for business hours, select **Customized Peak (ConfigMgr)** from the **Peak plan** list, and then select **Edit**. If you want to configure a power plan for non-business hours, select **Customized Non-Peak (ConfigMgr)** from the **Non-peak plan** list, and then select **Edit**.

    > [!NOTE]
    > You can use the **Computer Activity** report to help you decide the schedules to use for peak and non-peak hours when you apply power plans to collections of computers. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).

    You can also select from the built-in power plans: **Balanced (ConfigMgr)**, **High Performance (ConfigMgr)**, and **Power Saver (ConfigMgr)**. Select **View** to display the properties of each power plan.

    > [!NOTE]
    > You can't modify the built-in power plans.

1. For the power plan properties, configure the following settings:

    - **Name:** Specify a name for this power plan or use the supplied default value.

    - **Description:** Specify an optional description to further describe the plan in the console.

    - **Specify the properties for this power plan:** Configure the power plan properties. For more information, see [Available power management plan settings](#BKMK_Plans).

        > [!IMPORTANT]
        > When the Configuration Manager client applies the power plan to the device, it applies the enabled settings. If you unselect a power setting in the policy, the value on the client computer doesn't change when it applies the power plan. This action also doesn't restore the power setting to its previous value before a power plan was applied.

1. Select **OK** to save and close the power plan properties.

1. Select **OK** to save and close the collection properties, and to apply the power plan.

## <a name="BKMK_Plans"></a> Available power plan settings

The following table lists the power management settings available in Configuration Manager. You can configure separate settings for when the computer is plugged in or running on battery power. Depending on the version of Windows you use, some settings might not be configurable.

> [!NOTE]
> Power settings that you don't configure keep their current value on client computers.

|Name|Description|
|----------|-----------------|
|**Turn off display after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before the display is turned off. If you don't want power management to turn off the display, specify a value of `0`.|
|**Sleep after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before it enters sleep. If you don't want the device to sleep, specify a value of `0`.|
|**Require a password on wakeup**|`Yes` specifies that a user has to unlock the computer when it wakes up.|
|**Power button action**|Specifies the action when you press the computer's power button: **Do nothing**, **Sleep**, **Hibernate**, or **Shut down**.|
|**Start menu power button**|Specifies the action when you press the computer's **Start** menu power button: **Sleep**, **Hibernate**, or **Shut down**.|
|**Sleep button action**|Specifies the action when you press the computer's **Sleep** button: **Do nothing**, **Sleep**, **Hibernate**, or **Shut down**.|
|**Lid close action**|Specifies the action when the user closes the lid of a portable computer: **Do nothing**, **Sleep**, **Hibernate**, and **Shut down**.|
|**Turn off hard disk after (minutes)**|Specifies the length of time, in minutes, that the computer's hard disk must be inactive before it's turned off. If you don't want power management to turn off the computer's hard disk, specify a value of `0`.|
|**Hibernate after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before it hibernates. If you don't want the device to hibernate, specify a value of `0`.|
|**Low battery action**|Specifies the action when the computer's battery reaches the specified low battery notification level: **Do nothing**, **Sleep**, **Hibernate**, or **Shut down**.|
|**Critical battery action**|Specifies the action when the computer's battery reaches the specified critical battery notification level. When it's *on battery*: **Sleep**, **Hibernate**, or **Shut down**. When it's *plugged in*: **Do nothing**, **Sleep**, **Hibernate**, or **Shut down**.|
|**Allow hybrid sleep**|`On` specifies that Windows saves a hibernation file when it enters sleep. If there's a power loss while it's asleep, Windows uses this file to restore the computer's state.<br /><br /> Hybrid sleep is designed for desktop computers. By default, it's not enabled on portable computers. Enabling hybrid sleep disables the hibernate functionality.|
|**Allow standby state when sleeping action**|`On` enables the computer to be on standby. This state still consumes some power, but enables the computer to wake faster. If this setting is `Off`, the computer can only hibernate or turn off.|
|**Required idleness to sleep (%)**|Specifies the percentage of idle time on the computer processor time required for the computer to enter sleep. For computers running Windows 7 and alter, this value is always `0`.|
|**Enable Windows wake up timer for desktop computers**|Set `Enable` to enable the built-in Windows timer to wake a desktop computer. When this timer wakes a desktop computer, it stays awake for 10 minutes by default. This time period allows the client to install any updates or to receive policy.<br /><br />Wakeup timers aren't supported on portable computers. This behavior prevents scenarios where they might wake when they're on limited battery power.|
