---
title: "Upgrade Windows to the latest version with System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby

---
# Upgrade Windows to the latest version with System Center Configuration Manager
This topic provides the steps in System Center Configuration Manager to upgrade an  operating system on a computer from Windows 7 or later to Windows 10. You can choose from different deployment methods, such as stand-alone media or Software Center. The Windows 10 in-place upgrade scenario:  
  
-   Upgrades the operating system on computers that currently run Windows 7, Windows 8, or Windows 8.1. You can also do build-to-build upgrades of Windows 10. For example, you can upgrade Windows 10 RTM to Windows 10, version 1511.  
  
-   Retains the applications, settings, and user data on the computer.  
  
-   Has no external dependencies, such as the Windows ADK.  
  
-   Is generally faster and more resilient than traditional operating system deployments.  
  
 Use the following sections to deploy operating systems over the network by using a task sequence.  
  
##  <a name="BKMK_Plan"></a> Plan  
  
-   **Review the limitations for the task sequence to upgrade an operating system**  
  
     Review the following requirements and limitations  for the task sequence to upgrade an operating system to make sure it meets your needs:  
  
    -   You should only add task sequence steps that are related to the core task of deploying operating systems and configuring computers after the image is installed. This includes steps that install packages, applications, or updates, and steps that run command lines, PowerShell, or set dynamic variables.  
  
    -   Review drivers and applications that are installed on computers to ensure they are compatible with Windows 10 before you deploy the upgrade task sequence.  
  
    -   The following tasks are not compatible with the  in-place upgrade and require you to use traditional operation system deployments:  
  
        -   Changing the computers domain membership or update Local Administrators.  
  
        -   Implementing a fundamental change on the computer, including disk partitioning, a changing an architecture from x86 to x64, implementing UEFI, or modifying the base operating system language.  
  
        -   You have custom requirements including using a custom base image, using 3<sup>rd</sup> party disk encryption, or require WinPE offline operations.  
  
-   **Plan for and implement  infrastructure requirements**  
  
     The only prerequisites for the upgrade scenario is that you have a distribution point available for the operating system upgrade package and any other packages that you include in the task sequence. For more information, see [Install or modify a distribution point](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md#bkmk_Iinstall).  
  
##  <a name="BKMK_Configure"></a> Configure  
  
1.  **Prepare the operating system upgrade package**  
  
     The Windows 10 upgrade package contains the source files necessary to upgrade the operating system on the destination computer. The upgrade package must be the same edition, architecture, and language as the clients that you will upgrade.  For more information, see [Manage operating system upgrade packages with System Center Configuration Manager](../../osd/deploy-use/manage-operating-system-upgrade-packages.md).  
  
2.  **Create a task sequence to upgrade the operating system**  
  
     Use the steps in [Create a task sequence to upgrade an operating system in System Center Configuration Manager](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) to automate the upgrade of the operating system.  
  
    > [!NOTE]  
    >  Typically you will use the steps in [Create a task sequence to upgrade an operating system in System Center Configuration Manager](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) to create a task sequence to upgrade an operating system to Windows 10. The task sequence includes the Upgrade Operating System step, as well as additional  recommended steps and groups to handle the end-to-end upgrade process. However, you can create a custom task sequence and add the [Upgrade Operating System](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) task sequence step to upgrade the operating system. This is the only step required to upgrade the operating system to Windows 10. If you choose this method, also add the [Restart Computer](../../osd/understand/task-sequence-steps.md#BKMK_RestartComputer) step after the Upgrade Operating System step to complete the upgrade. Be sure to use the **The currently installed default operating system** setting to restart the computer  into the installed operating system and not Windows PE.  
  
##  <a name="BKMK_Deploy"></a> Deploy  
  
-   Use one of the following deployment methods to deploy the operating system:  
  
    -   [Use Software Center to deploy Windows over the network with System Center Configuration Manager](../../osd/deploy-use/use-software-center-to-deploy-windows-over-the-network.md)  
  
    -   [Use stand-alone media to deploy Windows without using the network in System Center Configuration Manager](../../osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  
  
## Monitor  
  
-   **Monitor the task sequence deployment**  
  
     To monitor the task sequence deployment  to upgrade the operating system, see [Monitor operating system deployments in System Center Configuration Manager](../../osd/deploy-use/monitor-operating-system-deployments.md).  
  
## See Also  
 [Scenarios to deploy enterprise operating systems with System Center Configuration Manager](../../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)

