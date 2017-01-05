---
title: Task sequence steps to manage BIOS to UEFI conversion | Configuration Manager
description: "Learn how to customize an operating system deployment task sequence to prepare a FAT32 partition for transition to UEFI."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Task sequence steps to manage BIOS to UEFI conversion
Starting in Configuration Manager version 1610, you can now customize an operating system deployment task sequence with a new variable, TSUEFIDrive, so that the **Restart Computer** step will prepare a FAT32 partition on the hard drive for transition to UEFI. The following procedure provides an example of how you can create task sequence steps to prepare the hard drive for the BIOS to UEFI conversion.

#### To prepare the FAT32 partition for the conversion to UEFI:
In an existing task sequence to install an operating system, you will add a new group with steps to do the BIOS to UEFI conversion.

1. Create a new task sequence group after the steps to capture files and settings, and before the steps to install the operating system. For example, create a group after the **Capture Files and Settings** group named **BIOS-to-UEFI**.
2. On the **Options** tab of the new group, add a new task sequence variable as a condition where **_SMSTSBootUEFI** is **not equal** to **true**. This prevents the steps in the group from running when a computer is already in UEFI mode.

   ![BIOS to UEFI group](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Under the new group, add the **Restart Computer** task sequence step. In **Specify what to run after restart**, select **The boot image assigned to this task sequence is selected** to start the computer in Windows PE.  
4. On the **Options** tab, add a task sequence variable as a condition where **_SMSTSInWinPE equals false**. This prevents this step from running if the computer is already in Windows PE.

	![Restart Computer step](../../core/get-started/media/restart-in-windows-pe.png)
5. Add a step to start the OEM tool that will convert the firmware from BIOS to UEFI. This will typically be a **Run Command Line** task sequence step with a command line to start the OEM tool.
6.	Add the Format and Partition Disk task sequence step that will partition and format the hard drive. In the step, do the following:
	1.	Create the FAT32 partition that will be converted to UEFI before the operating system is installed. Choose **GPT** for **Disk type**.

	   ![Format and partition disk step](../media/format-and-partition-disk.png)
	2.	Go to the properties for the FAT32 partition. Enter **TSUEFIDrive** in the **Variable** field. When the task sequence detects this variable, it will prepare for the UEFI transition before restarting the computer.

	   ![Partition properties](../../core/get-started/media/partition-properties.png)
	3. Create an NTFS partition that the task sequence engine uses to save its state and to store log files.
7.	Add the **Restart Computer** task sequence step. In **Specify what to run after restart**, select **The boot image assigned to this task sequence is selected** to start the computer in Windows PE.  
