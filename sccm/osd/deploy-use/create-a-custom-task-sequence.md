---
title: Create a custom task sequence
titleSuffix: Configuration Manager
description: Edit a custom task sequence in System Center Configuration Manager to add steps to the task sequence.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create a custom task sequence with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When you create a custom task sequence in System Center Configuration Manager, it contains no task sequence steps. After you create the task sequence, you must edit it and add the task sequence steps you need.  

##  <a name="BKMK_CustomTS"></a> Create a custom task sequence  
 Use the following procedure to create a custom task sequence.  

#### To create a custom task sequence  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, select **Create a new custom task sequence**.  

5.  On the **Task Sequence Information** page, specify a name for the task sequence, a description of the task sequence, and an optional boot image for the task sequence to use, and then complete the wizard.  

 After you complete the Create Task Sequence Wizard,  Configuration Manager adds the custom task sequence to the **Task Sequences** node. You can now edit this task sequence to add task sequence steps to it.  

 For a list of available task sequence steps, see [Task sequence steps](../understand/task-sequence-steps.md).  

 For more information about how to edit a task sequence, see [Edit a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Most often you will use task sequences to automate tasks for operating system deployment, but you can create a custom task sequence to automate a variety of tasks. For more information, see [Create a task sequence for non-operating system deployments](create-a-task-sequence-for-non-operating-system-deployments.md).  

 ## Next steps
 [Deploy the task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
