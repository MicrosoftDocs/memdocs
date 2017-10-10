---
title: Create a task sequence to capture and restore user state
titleSuffix: "Configuration Manager"
description: "Use System Center Configuration Manager task sequences to capture and restore the user-state data in operating system deployment scenarios."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: 7
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Create a task sequence to capture and restore user state in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can use System Center Configuration Manager task sequences to capture and restore the user state data in operating system deployment scenarios where you want to retain the user state of the current operating system. Depending on the type of task sequence you create, the capture and restore steps might be automatically added as part of the task sequence. In other scenarios, you might need to manually add the capture and restore steps to the task sequence. This topic provides the steps that you must add to an existing task sequence to capture and restore user state data.  

##  <a name="BKMK_CaptureRestoreUserState"></a> How to capture and restore user state data  
 To capture and restore the user state, you must add the following steps to the  task sequence:  

-   **Request State Store**: This step is needed only if you store the user state on the state migration point.  

-   **Capture User State**: This step captures the user state data and stores it on the state migration point or locally using links.  

-   **Restore User State**: This step restores the user state data on the destination computer. It can retrieve the data from a user state migration point or from the destination computer.  

-   **Release State Store**: This step is needed only if you store the user state on the state migration point. This step removes this data from the state migration point.  

 Use the following procedures to add the task sequence steps needed to capture the user state and restore the user state. For more information about creating a task sequences, see [Manage task sequences to automate tasks](manage-task-sequences-to-automate-tasks.md).  

#### To add task sequence steps to capture the user state  

1.  In the **Task Sequence** list, select a task sequence, and then click **Edit**.  

2.  If you are using a state migration point to store the user state, add the **Request State Store** step to the task sequence. In the **Task Sequence Editor** dialog box, click **Add**, point to **User State**, and then click **Request State Store**. Specify the following properties and options for the **Request State Store** step, and then click **Apply**.  

     On the **Properties** tab, specify the following options:  

    -   Enter a name and description for the step.  

    -   Click **Capture state from the computer**.  

    -   In the **Number of retries** box, specify the number of times the task sequence attempts to capture the user state data if an error occurs.  

    -   In the **Retry delay (in seconds)** box, specify how many seconds that the task sequence waits before it retries to capture the data.  

    -   Select the **If computer account fails to connect to state store, use the Network Access account** check box to specify whether to use the Configuration Manager [Network Access Account](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) to connect to the state store.  

     On the **Options** tab, specify the following options:  

    -   Select the **Continue on error** check box if you want the task sequence to continue to the next step if this step fails.  

    -   Specify any conditions that must be met before the task sequence can continue if an error occurs.  

3.  Add the **Capture User State** step to the task sequence. In the **Task Sequence Editor** dialog box, click **Add**, point to **User State**, and then click **Capture User State**. Specify the following properties and options for the **Capture User State** step, and then click **OK**.  

    > [!IMPORTANT]  
    >  When you add this step to your task sequence, also set the **OSDStateStorePath** task sequence variable to specify where the user state data is stored. If you store the user state locally, do not specify a root folder as that can cause the task sequence to fail. When you store the user data locally always use a folder or subfolder. For information about this variable, see [Capture User State Task Sequence Action Variables](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     On the **Properties** tab, specify the following options:  

    -   Enter a name and description for the step.  

    -   Specify the package that contains the USMT source file used to capture the user state data.  

    -   Specify the user profiles to capture:  

        -   Click **Capture all user profiles with standard options** to capture all user profiles.  

        -   Click **Customize user profile capture** to specify individual user profiles to capture. Select the configuration file (miguser.xml, migsys.xml, or migapp.xml) that contains the user profile information. You cannot use the config.xml configuration file here, but you can manually add it to the USMT command line using the OSDMigrageAdditionalCaptureOptions and OSDMigrateAdditionalRestoreOptions variables.

    -   Select **Enable verbose logging** to specify how much information to write to log files if an error occurs.  

    -   Select **Skip files that use the Encrypting File System (EFS)**.  

    -   Select **Copy by using file system access** to specify the following settings:  

        -   **Continue if some files cannot be captured**: This setting allows the task sequence step to continue the migration process even if some files cannot be captured. If you disable this option and a file cannot be captured, the task sequence step fails. This option is enabled by default.  

        -   **Capture locally by using links instead of by copying files**: This setting allows you to use the hard link migration feature that is available in USMT 4.0. This setting is ignored if you use versions of USMT that are earlier than USMT 4.0.  

        -   **Capture in off-line mode (Windows PE only)**: This setting allows you to capture use state from Windows PE without booting to the existing operating system. This setting is ignored if you use versions of USMT that are earlier than USMT 4.0.  

    -   Select **Capture by using Volume Copy Shadow Services (VSS)**. This setting is ignored if you use versions of USMT that are earlier than USMT 4.0.  

     On the **Options** tab, specify the following options:  

    -   Select the **Continue on error** check box if you want the task sequence to continue to the next step if this step fails.  

    -   Specify any conditions that must be met before the task sequence can continue if an error occurs.  

4.  If you are using a state migration point to store the user state, add the [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) step to the task sequence. In the **Task Sequence Editor** dialog box, click **Add**, point to **User State**, and then click **Release State Store**. Specify the following properties and options for the **Release State Store** step, and then click **OK**.  

    > [!IMPORTANT]  
    >  The task sequence action that runs before the **Release State Store** step must be successful before the **Release State Store** step is started.  

     On the **Properties** tab, enter a name and description for the step.  

     On the **Options** tab, specify the following options.  

    -   Select the **Continue on error** check box if you want the task sequence to continue to the next step if this step fails.  

    -   Specify any conditions that must be met before the task sequence can continue when an error occurs.  

 Deploy this task sequence to capture the user state on a destination computer. For information about how to deploy task sequences, see [Deploy a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### To add task sequence steps to restore the user state  

1.  In the **Task Sequence** list, select a task sequence, and then click **Edit**.  

2.  Add the [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) step to the task sequence. In the **Task Sequence Editor** dialog box, click **Add**, point to **User State**, and then click **Restore User State**. This step establishes a connection to the state migration point. Specify the following properties and options for the **Restore User State** step, and then click **OK**.  

     On the **Properties** tab, specify the following properties:  

    -   Enter a name and description for the step.  

    -   Specify the package that contains the USMT to restore the user state data.  

    -   Specify the user profiles to restore:  

        -   Click **Restore all captured user profiles with standard options** to restore all user profiles.  

        -   Click **Customize user profile restore** to restore individual user profiles. Select the configuration file (miguser.xml, migsys.xml, or migapp.xml) that contains the user profile information. You cannot use the config.xml configuration file here, but you can manually add it to the USMT command line using the OSDMigrageAdditionalCaptureOptions and OSDMigrateAdditionalRestoreOptions variables.

    -   Select **Restore local computer user profiles** to provide a new password for the restored profiles. You cannot migrate passwords for local profiles.  

        > [!NOTE]  
        >  When you have local user accounts, and you use the [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) step and select **Capture all user profiles with standard options**, you must select the **Restore local computer user profiles** setting in the [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) step or the task sequence will fail.  

    -   Select **Continue if some files cannot be restored** if you want the **Restore User State** step to continue if a file cannot be restored.  

         If you store the user state by using local links and the restore is not successful, the administrative user can manually delete the hard-links that were created to store the data or the task sequence can run the USMTUtils tool. If you use USMTUtils to delete the hard-link, add a [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) step after you run USMTUtils.  

    -   Select **Enable verbose logging** to specify how much information to write to log files if an error occurs.  

     On the **Options** tab, specify the following options:  

    -   Select the **Continue on error** check box if you want the task sequence to continue to the next step if this step fails.  

    -   Specify any conditions that must be met before the task sequence can continue if an error occurs.  

3.  If you are using a state migration point to store the user state, add the [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) step to the task sequence. In the **Task Sequence Editor** dialog box, click **Add**, point to **User State**, and then click **Release State Store**. Specify the following properties and options for the **Release State Store** step, and then click **OK**.  

    > [!IMPORTANT]  
    >  The task sequence action that runs before the **Release State Store** step must be successful before the **Release State Store** step is started.  

     On the **Properties** tab, enter a name and description for the step.  

     On the **Options** tab, specify the following options.  

    -   Select the **Continue on error** check box if you want the task sequence to continue to the next step if this step fails.  

    -   Specify any conditions that must be met before the task sequence can continue when an error occurs.  

 Deploy this task sequence to restore the user state on a destination computer. For information about deploying task sequences, see [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## Next steps
[Monitor the task sequence deployment](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
