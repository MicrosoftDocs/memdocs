---
title: Create a task sequence for non-OS deployments
titleSuffix: Configuration Manager
description: Create task sequences that aren't for deploying an OS, such as distributing software or automating tasks
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create a task sequence for non-OS deployments

*Applies to: Configuration Manager (current branch)*

Task sequences in Configuration Manager are used to automate different kinds of tasks within your environment. These tasks are primarily designed and tested for deploying operating systems. Configuration Manager has many other features that should be the primary technology that you use for the following scenarios:

- [Application installation](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Starting in version 2002, install complex applications using task sequences via the application model. Add a deployment type to an app that's a task sequence, either to install or uninstall the app. For more information, see [Create Windows applications](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Software updates installation](../../sum/understand/software-updates-introduction.md)

- [Setting configuration](../../compliance/understand/ensure-device-compliance.md)

Also consider other Microsoft System Center automation technologies, such as [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) and [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

The power of task sequences lies in their flexibility and how you use them. They can configure client settings, distribute software, update drivers, edit user states, and do other tasks independent of OS deployment. You can create a custom task sequence to add any number of tasks. The use of custom task sequences for non-OS deployment is supported in Configuration Manager. However, if a task sequence results in unwanted or inconsistent results, look at ways to simplify the operation:

- Use simpler steps
- Divide the actions across multiple task sequences
- Take a phased approach to creating and testing the task sequence

The following steps are supported for use in a non-OS deployment custom task sequence:  

- [Check Readiness](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Connect To Network Folder](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Install Application](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Install Software Updates](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Run Task Sequence](../understand/task-sequence-steps.md#child-task-sequence)  

- [Set Dynamic Variables](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Set Task Sequence Variable](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
