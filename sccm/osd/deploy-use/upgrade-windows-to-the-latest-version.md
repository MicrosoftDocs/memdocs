---
title: Upgrade Windows to the latest version
description: "Learn how to use Configuration Manager to upgrade an operating system from Windows 7 or later to Windows 10."
ms.custom: na
ms.date: 02/06/2017
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
ms.author: dougeby
manager: angrobe

---
# Upgrade Windows to the latest version with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic provides the steps in System Center Configuration Manager to upgrade an  operating system on a computer from Windows 7 or later to Windows 10, or from Windows Server 2012 to Windows Server 2016, on a destination computer. You can choose from different deployment methods, such as stand-alone media or Software Center. The in-place upgrade scenario:  

-   Upgrades the operating system on computers that currently run:
    - Windows 7, Windows 8, or Windows 8.1. You can also do build-to-build upgrades of Windows 10. For example, you can upgrade Windows 10 RTM to Windows 10, version 1511.  
    - Windows Server 2012. You can also do build-to-build upgrades of Windows Server 2016. For details about supported upgrade paths, see [Supported upgrade paths](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Retains the applications, settings, and user data on the computer.  

-   Has no external dependencies, such as the Windows ADK.  

-   Is faster and more resilient than traditional operating system deployments.  

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

-   **Plan for and implement infrastructure requirements**  

     The only prerequisites for the upgrade scenario are that you have a distribution point available for the operating system upgrade package and any other packages that you include in the task sequence. For more information, see [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="BKMK_Configure"></a> Configure  

1.  **Prepare the operating system upgrade package**  

     The Windows 10 upgrade package contains the source files necessary to upgrade the operating system on the destination computer. The upgrade package must be the same edition, architecture, and language as the clients that you upgrade.  For more information, see [Manage operating system upgrade packages](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Create a task sequence to upgrade the operating system**  

     Use the steps in [Create a task sequence to upgrade an operating system](create-a-task-sequence-to-upgrade-an-operating-system.md) to automate the upgrade of the operating system.  

    > [!IMPORTANT]
    > When you use stand-alone media, you must include a boot image in the task sequence for it to be available in the Task Sequence Media Wizard.

    > [!NOTE]  
    > Typically you use the steps in [Create a task sequence to upgrade an operating system](create-a-task-sequence-to-upgrade-an-operating-system.md) to create a task sequence to upgrade an operating system to Windows 10. The task sequence includes the Upgrade Operating System step, as well as additional recommended steps and groups to handle the end-to-end upgrade process. However, you can create a custom task sequence and add the [Upgrade Operating System](../understand/task-sequence-steps.md#BKMK_UpgradeOS) task sequence step to upgrade the operating system. This is the only step required to upgrade the operating system to Windows 10. If you choose this method, also add the [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) step after the Upgrade Operating System step to complete the upgrade. Be sure to use the **The currently installed default operating system** setting to restart the computer into the installed operating system and not Windows PE.  

##  <a name="BKMK_Deploy"></a> Deploy  

-   Use one of the following deployment methods to deploy the operating system:  

    -   [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## Monitor  

-   **Monitor the task sequence deployment**  

     To monitor the task sequence deployment  to upgrade the operating system, see [Monitor operating system deployments](monitor-operating-system-deployments.md).  
