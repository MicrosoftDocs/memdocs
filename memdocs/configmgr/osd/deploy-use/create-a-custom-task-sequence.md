---
title: Create a custom task sequence
titleSuffix: Configuration Manager
description: Edit a custom task sequence in Configuration Manager to add steps to the task sequence.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create a custom task sequence with Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you create a custom task sequence in Configuration Manager, it contains no task sequence steps. After you create the task sequence, edit it, and add the task sequence steps you need.  

## <a name="BKMK_CustomTS"></a> Create a custom task sequence

Use the following procedure to create a custom task sequence:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Task Sequences** node.  

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence**. This action starts the Create Task Sequence Wizard.  

1. On the **Create a New Task Sequence** page, select **Create a new custom task sequence**.  

1. On the **Task Sequence Information** page, specify:

    - A name for the task sequence
    - A description of the task sequence
    - An optional boot image for the task sequence to use

After you complete the Create Task Sequence Wizard, Configuration Manager adds the custom task sequence to the **Task Sequences** node. You can now edit this task sequence to add task sequence steps to it.  

## See also

For a list of available task sequence steps, see [Task sequence steps](../understand/task-sequence-steps.md).  

For more information about how to edit a task sequence, see [Use the task sequence editor](../understand/task-sequence-editor.md).  

Most often you'll use task sequences to automate tasks for OS deployment, but you can create a custom task sequence to automate different kinds of tasks. For more information, see [Create a task sequence for non-OS deployments](create-a-task-sequence-for-non-operating-system-deployments.md).

Starting in version 2002, install complex applications using task sequences via the application model. Add a deployment type to an app that's a task sequence, either to install or uninstall the app. For more information, see [Create Windows applications](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## Next steps

[Deploy the task sequence](deploy-a-task-sequence.md)
