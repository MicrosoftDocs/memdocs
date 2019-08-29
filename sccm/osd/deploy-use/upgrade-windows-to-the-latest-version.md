---
title: Upgrade to Windows 10
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to upgrade an OS from Windows 7 or later to Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Upgrade Windows to the latest version with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides the steps in Configuration Manager to upgrade the OS on a computer. You can choose from different deployment methods, such as stand-alone media or Software Center. The in-place upgrade scenario has the following features:  

- Upgrades the OS to Windows 10, or Windows Server 2016 and later

- Keeps the applications, settings, and user data on the computer

- Has no external dependencies, such as the Windows ADK

- Is faster and more resilient than traditional OS deployments

> [!Note]  
> The Windows 10 in-place upgrade task sequence supports deployment to internet-based clients managed through the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the intranet. For more information, see [Deploy Windows 10 in-place upgrade via CMG](/sccm/osd/deploy-use/deploy-a-task-sequence#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## Supported versions

### Upgrade version

Only create OS upgrade packages to upgrade to the following OS versions:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### Original version

Devices must run one of the following OS versions to target an OS upgrade task sequence:

#### Windows client

- Windows 7
- Windows 8.1
- An earlier version of Windows 10. For example, you can upgrade Windows 10, version 1809 to Windows 10, version 1903.  

For more information, see [Windows 10 upgrade paths](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths).

#### Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- An earlier version of Windows Server 2016
- An earlier version of Windows Server 2019

For more information about Windows Server supported upgrade paths, see [Windows Server 2016 supported upgrade paths](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) and [Windows Server Upgrade Center](http://aka.ms/upgradecenter).


## <a name="BKMK_Plan"></a> Plan  

### Task sequence requirements and limitations

Review the following requirements and limitations for the task sequence to upgrade an OS to make sure it meets your needs:  

- Only add task sequence steps that are related to the core task of upgrading the OS. These steps primarily include installing packages, applications, or updates. Also use steps that run command lines, PowerShell, or set dynamic variables.  

- Review drivers and applications that are installed on computers. Before you deploy the upgrade task sequence, make sure the drivers are compatible with Windows 10.  

The following tasks aren't compatible with the in-place upgrade. They require you to use traditional OS deployments:  

- Changing the computer's domain membership, or updating the local Administrators group.  

- Implementing a fundamental change on the computer, such as:

  - Changing disk partitions
  - Changing the system architecture from x86 to x64
  - Implementing UEFI. (For more information on a possible option, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
  - Modifying the base OS language  

- You have custom requirements including using a custom base image, using third-party disk encryption, or require WinPE offline operations.  

### Infrastructure requirements  

The only prerequisite for the upgrade scenario is to have a distribution point available. Distribute the OS upgrade package and any other packages that you include in the task sequence. For more information, see [Install or modify a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).


## <a name="BKMK_Configure"></a> Configure  

### Prepare the OS upgrade package  

The Windows 10 upgrade package contains the source files necessary to upgrade the OS on the destination computer. The upgrade package must be the same edition, architecture, and language as the clients that you upgrade. For more information, see [Manage OS upgrade packages](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

### Create a task sequence to upgrade the OS  

Use the steps in [Create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) to automate the upgrade of the OS.  

> [!NOTE]  
> To create a task sequence to upgrade an OS to Windows 10, you typically use the steps in [Create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system). The task sequence includes the **Upgrade OS** step, as well as additional recommended steps and groups to handle the end-to-end upgrade process.
>
> You can create a custom task sequence and add the [Upgrade OS](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS) step. This step is the only one required to upgrade the OS to Windows 10. If you choose this method, to complete the upgrade, also add the [Restart Computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) step after the **Upgrade OS** step. Be sure to use the **The currently installed default operating system** setting to restart the computer into the installed OS and not Windows PE.  


## <a name="BKMK_Deploy"></a> Deploy  

To deploy the OS, use one of the following deployment methods:  

- [Use Software Center to deploy Windows over the network](/sccm/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network)  

- [Use stand-alone media to deploy Windows without using the network](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network)  

  > [!IMPORTANT]  
  > When you use stand-alone media, you must include a boot image in the task sequence. This configuration makes the task sequence available in the Task Sequence Media Wizard.


## Monitor  

To monitor the task sequence deployment to upgrade the OS, see [Monitor OS deployments](/sccm/osd/deploy-use/monitor-operating-system-deployments).  
