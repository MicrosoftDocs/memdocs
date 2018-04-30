---
title: Create a task sequence for non-operating system deployments
titleSuffix: Configuration Manager
description: Create task sequences that are not related to deploying operating systems, such as distributing software, updating drivers, editing user states, etc.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create a task sequence for non-operating system deployments with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Task sequences in System Center Configuration Manager are used to automate a variety of tasks within your environment. These tasks are primarily designed and tested for deploying operating systems.  Configuration Manager has many other features that should be the primary technology that you use for scenarios such as [application installation](../../apps/understand/introduction-to-application-management.md), [software updates installation](../../sum/understand/software-updates-introduction.md), [setting configuration](../../compliance/understand/ensure-device-compliance.md), or custom automation. There are other Microsoft System Center automation technologies, such as [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) and [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) that you should also consider.  

The power of task sequences lies in their flexibility and how you can use them to configure client settings, distribute software, update drivers, edit user states, and perform other tasks independent of operating system deployment. You can create a custom task sequence to add any number of tasks. The use of custom task sequences for non-operating system deployment is supported in Configuration Manager. However, if a task sequence results in unwanted or inconsistent results, look at ways to simplify the operation. You can accomplish this by using simpler steps, dividing the actions across multiple task sequences, or by taking a phased approach to creating and testing the task sequence.

 The following steps are supported for use in a non-operating system deployment custom task sequence:  

-   [Check Readiness](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Connect To Network Folder](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Install Application](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Install Software Updates](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Set Dynamic Variables](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Set Task Sequence Variable](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## Next steps 
[Deploy the task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
