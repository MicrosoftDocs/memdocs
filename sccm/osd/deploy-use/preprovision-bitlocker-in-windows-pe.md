---
title: Preprovision BitLocker in Windows PE
titleSuffix: "Configuration Manager"
description: "The Preprovision BitLocker task in Configuration Manager enables BitLocker from the Windows Preinstallation Environment before operating system deployment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Preprovision BitLocker in Windows PE with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
The **Pre-provision BitLocker** task sequence step in System Center Configuration Manager allows you to enable BitLocker from the Windows Preinstallation Environment (Windows PE) prior to operating system deployment. Only the used drive space is encrypted, and therefore, encryption times are much faster. This is done with a randomly generated clear protector applied to the formatted volume and encrypting the volume prior to running the Windows setup process. The ability to pre-provision BitLocker was introduced with Windows 8 and Windows Server 2012. However, you can pre-provision BitLocker on a hard drive and install Windows 7 as long as you follow specific steps. After Windows 7 Setup completes, you must set a BitLocker key protector because the Windows 7 BitLocker control panel does not support BitLocker with a clear protector. You must add a key protector by using the **Enable BitLocker** step or by using the manage-bde.exe command-line tool.  

 Generally, you must do the following to successfully pre-provision BitLocker on a computer that will install Windows 7:  

-   Restart the computer in Windows PE  

    > [!IMPORTANT]  
    >  You must use a boot image with Windows PE 4 or later to pre-provision BitLocker. For more information about supported Windows PE versions in Configuration Manager, see [Dependencies External to Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

-   Partition and format the hard drive  

-   Pre-provision BitLocker  

-   Install Windows 7 with specific operating system and network settings  

-   Add a key protector to BitLocker  

 In Configuration Manager, the recommended way to pre-provision BitLocker on a hard drive and install Windows 7 is to create a new task sequence and select **Install an existing image package** from the **Create New Task Sequence** page of the **Create Task Sequence Wizard**. The wizard creates the task sequence steps listed in following table.  

> [!NOTE]  
>  The task sequence might have additional steps depending on how you configured the settings in the wizard. For example, you might have the **Capture Windows Settings** step if you selected **Captured Microsoft Windows settings** on the **State Migration** page of the wizard.  

|Task sequence step|Details|  
|------------------------|-------------|  
|Disable BitLocker|This step disables BitLocker encryption, if it is currently enabled. For more information, see [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Restart Computer in Windows PE|This step restarts the computer in Windows PE by running the boot image assigned to the task sequence. You must use a boot image with Windows PE 4 or later to pre-provision BitLocker. For more information, see [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Partition Disk 0 - BIOS<br /><br /> Partition Disk 0 - UEFI|These steps format and partition the specified drive on the destination computer by using BIOS or UEFI. The task sequence uses UEFI when it detects that the destination computer is in UEFI mode. For more information, see [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Pre-provision BitLocker|This step enables BitLocker on a drive while in Windows PE. Only the used drive space is encrypted. Because you partitioned and formatted the hard drive in the previous step, there is no data, and encryption completes very quickly. For more information, see [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Apply Operating System|This step prepares the answer file that is used to install the operating system on the destination computer and sets the OSDTargetSystemDrive task sequence variable to the drive letter of the partition that contains the operating system files. The answer file and variable are used by the Setup Windows and ConfigMgr step to install the operating system. For more information, see [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Apply Windows Settings|This step adds Windows settings to the answer file. The answer file is used by the Setup Windows and ConfigMgr step to install the operating system. For more information, see [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Apply Network Settings|This step adds Network settings to the answer file. The answer file is used by the Setup Windows and ConfigMgr step to install the operating system. For more information, see [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Apply Device Drivers|This step matches and installs drivers as part of the operating system deployment. For more information, see [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Setup Windows and ConfigMgr|This step performs the transition from Windows PE to the new operating system. This task sequence step is a required part of any operating system deployment. It installs the Configuration Manager client into the new operating system and prepares for the task sequence to continue execution in the new operating system. For more information, see [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Enable BitLocker|This step enables BitLocker encryption on the hard drive and sets key protectors. Because the hard drive was pre-provisioned with BitLocker, this step completes very quickly. Windows 7 requires that you add a key protector. If you do not use this step, you can run the manage-bde.exe command-line tool to set a key protector. For more information, see [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
