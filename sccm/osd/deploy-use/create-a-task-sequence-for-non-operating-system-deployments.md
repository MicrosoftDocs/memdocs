---
title: Create a task sequence for non-OS deployments
titleSuffix: Configuration Manager
description: Create task sequences that aren't for deploying an OS, such as distributing software or automating tasks
ms.date: 05/03/2019
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

- [Application installation](/sccm/apps/understand/introduction-to-application-management)
- [Software updates installation](/sccm/sum/understand/software-updates-introduction)
- [Setting configuration](/sccm/compliance/understand/ensure-device-compliance)

Also consider other Microsoft System Center automation technologies, such as [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) and [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

The power of task sequences lies in their flexibility and how you use them. They can configure client settings, distribute software, update drivers, edit user states, and do other tasks independent of OS deployment. You can create a custom task sequence to add any number of tasks. The use of custom task sequences for non-OS deployment is supported in Configuration Manager. However, if a task sequence results in unwanted or inconsistent results, look at ways to simplify the operation:

- Use simpler steps
- Divide the actions across multiple task sequences
- Take a phased approach to creating and testing the task sequence

The following steps are supported for use in a non-OS deployment custom task sequence:  

- [Check Readiness](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [Connect To Network Folder](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [Download Package Content](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [Install Application](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [Install Package](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [Install Software Updates](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [Restart Computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [Run Command Line](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [Run PowerShell Script](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [Run Task Sequence](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [Set Dynamic Variables](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  
