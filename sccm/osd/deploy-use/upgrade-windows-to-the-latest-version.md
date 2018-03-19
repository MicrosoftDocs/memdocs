---
title: Upgrade to Windows 10
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to upgrade an OS from Windows 7 or later to Windows 10.
ms.custom: na
ms.date: 03/21/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Upgrade Windows to the latest version with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides the steps in Configuration Manager to upgrade the OS on a computer. You can choose from different deployment methods, such as stand-alone media or Software Center. The in-place upgrade scenario has the following features:  

-   Upgrades the OS on computers that currently run:
    - Windows 7, Windows 8, or Windows 8.1. You can also do build-to-build upgrades of Windows 10. For example, you can upgrade Windows 10 version 1607 to Windows 10, version 1709.  
    
    - Windows Server 2012. You can also do build-to-build upgrades of Windows Server 2016. For more information about supported upgrade paths, see [Supported upgrade paths](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Retains the applications, settings, and user data on the computer.  

-   Has no external dependencies, such as the Windows ADK.  

-   Is faster and more resilient than traditional OS deployments.  


> [!Note]  
> Starting in version 1802, the Windows 10 in-place upgrade task sequence supports deployment to internet-based clients managed through the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the intranet. For more information, see [Deploy Windows 10 in-place upgrade via CMG](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Plan  

### Task sequence requirements and limitations

Review the following requirements and limitations for the task sequence to upgrade an OS to make sure it meets your needs:  

  -   Only add task sequence steps that are related to the core task of upgrading the OS. These steps primarily include installing packages, applications, or updates. Also use steps that run command lines, PowerShell, or set dynamic variables.  

  -   Review drivers and applications that are installed on computers to ensure they are compatible with Windows 10 before you deploy the upgrade task sequence.  

  -   The following tasks are not compatible with the in-place upgrade. They require you to use traditional OS deployments:  

     -   Changing the computer's domain membership, or updating the local Administrators group.  

     -   Implementing a fundamental change on the computer, such as: 
         - Changing disk partitions
         - Changing the system architecture from x86 to x64
         - Implementing UEFI. (For more information on a possible option, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
         - Modifying the base OS language  

     -   You have custom requirements including using a custom base image, using third-party disk encryption, or require WinPE offline operations.  

### Infrastructure requirements  

The only prerequisite for the upgrade scenario is to have a distribution point available. Distribute the OS upgrade package and any other packages that you include in the task sequence. For more information, see [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Configure  

### Prepare the OS upgrade package  

  The Windows 10 upgrade package contains the source files necessary to upgrade the OS on the destination computer. The upgrade package must be the same edition, architecture, and language as the clients that you upgrade. For more information, see [Manage operating system upgrade packages](../get-started/manage-operating-system-upgrade-packages.md).  


### Create a task sequence to upgrade the OS  

  Use the steps in [Create a task sequence to upgrade an operating system](create-a-task-sequence-to-upgrade-an-operating-system.md) to automate the upgrade of the OS.  

   > [!NOTE]  
   > Typically you use the steps in [Create a task sequence to upgrade an operating system](create-a-task-sequence-to-upgrade-an-operating-system.md) to create a task sequence to upgrade an OS to Windows 10. The task sequence includes the Upgrade Operating System step, as well as additional recommended steps and groups to handle the end-to-end upgrade process. However, you can create a custom task sequence and add the [Upgrade Operating System](../understand/task-sequence-steps.md#BKMK_UpgradeOS) task sequence step to upgrade the OS. This step is the only one required to upgrade the OS to Windows 10. If you choose this method, also add the [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) step after the Upgrade Operating System step to complete the upgrade. Be sure to use the **The currently installed default operating system** setting to restart the computer into the installed OS and not Windows PE.  



##  <a name="BKMK_Deploy"></a> Deploy  

To deploy the OS, use one of the following deployment methods:  

  -   [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > When you use stand-alone media, you must include a boot image in the task sequence for it to be available in the Task Sequence Media Wizard.




## Monitor  

To monitor the task sequence deployment to upgrade the OS, see [Monitor operating system deployments](monitor-operating-system-deployments.md).  
