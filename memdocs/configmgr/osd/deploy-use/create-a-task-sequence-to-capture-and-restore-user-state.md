---
title: Capture and restore user state
titleSuffix: Configuration Manager
description: Use Configuration Manager task sequences to capture and restore the user state data in OS deployment scenarios.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create a task sequence to capture and restore user state in Configuration Manager

 *Applies to: Configuration Manager (current branch)*

 Use Configuration Manager task sequences to capture and restore the user state data in OS deployment scenarios. In these scenarios, you want to retain the user state of the current OS. Depending on the type of task sequence you create, the capture and restore steps might be automatically added as part of the task sequence. In other scenarios, you might need to manually add the capture and restore steps to the task sequence. This article provides the steps that you must add to an existing task sequence to capture and restore user state data.  



## Task sequence steps  

To capture and restore the user state, add the following steps to the task sequence:  

- [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore): If you store the user state on the state migration point, you need this step.  

- [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState): This step captures the user state data. It then stores the data on either the state migration point or the local disk using hardlinks.  

- [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState): This step restores the user state data on the destination computer. It can retrieve the data from a state migration point or if hardlinked on the local disk.  

- [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): If you store the user state on the state migration point, you need this step. This step removes the data from the state migration point.  


 Use the following procedures to add the task sequence steps needed to capture and restore the user state. For more information about creating a task sequence, see [Manage task sequences to automate tasks](manage-task-sequences-to-automate-tasks.md).  



## Capture the user state  

 To add task sequence steps to capture the user state, use the following steps:

1.  In the **Task Sequence** list, select a task sequence, and then click **Edit**.  

2.  If you're using a state migration point to store the user state, add the **Request State Store** step to the task sequence. In the **Task Sequence Editor**, click **Add**. Point to **User State**, and then click **Request State Store**. Configure the properties and options for this step, and then click **Apply**. For more information about the available settings, see [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Add the **Capture User State** step to the task sequence. In the **Task Sequence Editor**, click **Add**. Point to **User State**, and then click **Capture User State**. Configure the properties and options for this step, and then click **Apply**. For more information about the available settings, see [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  When you add this step to your task sequence, also set the **OSDStateStorePath** task sequence variable to specify where to store the user state data. If you store the user state locally, don't specify a root folder as that can cause the task sequence to fail. When you store the user data locally always use a folder or subfolder. For more information about this variable, see [Task sequence variables](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  If you're using a state migration point, add the **Release State Store** step to the task sequence. In the **Task Sequence Editor**, click **Add**. Point to **User State**, and then click **Release State Store**. Configure the properties and options for this step, and then click **Apply**. For more information about the available settings, see [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  The task sequence action that runs before the **Release State Store** step must be successful before the **Release State Store** step starts.  


 Deploy this task sequence to capture the user state on a destination computer. For information about how to deploy task sequences, see [Deploy a task sequence](deploy-a-task-sequence.md).  



## Restore the user state  

 To add task sequence steps to restore the user state, use the following steps:

1. In the **Task Sequence** list, select a task sequence, and then click **Edit**.  

2. Add the **Restore User State** step to the task sequence. In the **Task Sequence Editor**, click **Add**. Point to **User State**, and then click **Restore User State**. This step establishes a connection to the state migration point if necessary. Configure the properties and options for this step, and then click **Apply**. For more information about the available settings, see [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  When you use the [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) step with the option to **Capture all user profiles with standard options**, you must select the **Restore local computer user profiles** setting in the **Restore User State** step. Otherwise the task sequence will fail.  

   > [!Note]  
   > If you store the user state by using local hardlinks and the restore isn't successful, you can manually delete the hardlinks that were created to store the data. The task sequence can run the USMTUtils tool to automate this action with a [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) step. If you use USMTUtils to delete the hardlink, add a [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) step after you run USMTUtils.  

3. If you're using a state migration point to store the user state, add the **Release State Store** step to the task sequence. In the **Task Sequence Editor**, click **Add**. Point to **User State**, and then click **Release State Store**. Configure the properties and options for this step, and then click **Apply**. For more information about the available settings, see [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  The task sequence action that runs before the **Release State Store** step must be successful before the **Release State Store** step starts.  


 Deploy this task sequence to restore the user state on a destination computer. For information about deploying task sequences, see [Deploy a task sequence](deploy-a-task-sequence.md).  



## Next steps

[Monitor the task sequence deployment](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
