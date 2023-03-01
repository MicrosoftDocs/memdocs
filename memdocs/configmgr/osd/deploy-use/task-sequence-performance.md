---
title: Task sequence performance
titleSuffix: Configuration Manager
description: To improve the overall speed of the task sequence, run it with the Windows high-performance power plan.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.localizationpriority: medium
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Task sequence performance

*Applies to: Configuration Manager (current branch)*

<!--3555926-->

To improve the overall speed of the task sequence, run it with the high-performance power plan. It configures Windows to use its built-in high-performance power plan, which delivers maximum performance at the expense of higher power consumption. This option is on by default for new task sequences.

When the task sequence starts, in most scenarios it records the currently enabled power plan. It then switches the active power plan to the Windows default **High Performance** plan. If the task sequence restarts the computer, it repeats this process. At the end of the task sequence, it resets the power plan to the stored value. This functionality works in both Windows and Windows PE, but has no effect on virtual machines.

- If the task sequence starts in Windows PE, the task sequence doesn't record the currently enabled power plan for later reuse.

- An OS deployment task sequence that reimages the computer (wipe and load) doesn't preserve the power plan setting of the old OS. At the end of the task sequence, it restores the default **Balanced** power plan.

You can use this option on devices with [modern standby](/windows-hardware/design/device-experiences/modern-standby).<!--7721999 & 8177793--> It also supports other devices that don't have that default power plan. When you use this task sequence option, it creates a temporary power plan that's similar to the default for **High Performance**. This power plan modifies the timeout values to `0` for standby, monitor, disk, and hibernate when plugged in. These configurations prevent these devices from falling asleep during an OS deployment task sequence.<!--MEMDocs#1646--> After the task sequence completes, it reverts to the original power plan, and deletes the temporary plan.

> [!IMPORTANT]
> To take advantage of this Configuration Manager feature, after you update the site, update clients to the latest version. Also update boot images to include the latest client components. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Configure the task sequence

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Operating Systems**, and select the **Task Sequences** node.

1. Select the task sequence to configure, and then in the ribbon select **Properties**.

1. Switch to the **More Options** tab.

    > [!TIP]
    > In version 2111 and earlier, this tab is named **Performance**.

1. Enable the option to **Run as high performance power plan**.

> [!WARNING]
> Be cautious with this setting on low performance hardware. Running intense system operations for an extended period of time can strain low-end hardware. Check with your hardware manufacturer for specific guidance.

## Known issues

<!-- 5554928 -->

Usually, when you change settings in task sequence properties, it updates all existing deployments. When you change this performance setting in the task sequence properties, it doesn't affect any existing deployments of the task sequence. To enable or disable this setting for high performance, create a new task sequence deployment.
<!-- MEMDocs#437, SCCMDocs#2107 -->

## Next steps

[Distribute referenced content](distribute-task-sequence-referenced-content.md)
