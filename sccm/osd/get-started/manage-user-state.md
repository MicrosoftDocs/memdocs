---
title: "Manage user state "
titleSuffix: "Configuration Manager"
description: "System Center Configuration Manager uses the User State Migration Tool to capture and restore user state data in operating system deployment scenarios."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
caps.latest.revision: 12
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Manage user state in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
You can use System Center Configuration Manager task sequences to capture and restore the user state data in operating system deployment scenarios where you want to retain the user state of the current operating system. For example:  

-   Deployments where you want to capture the user state from one computer to restore it on another computer.  

-   Update deployments where you want to capture and restore the user state on the same computer.  

 Configuration Manager uses the User State Migration Tool (USMT) 10.0 to manage the migration of user state data from a source computer to a destination computer after the operating system installation completes. For more information about common migration scenarios for the USMT 10.0, see  [Common Migration Scenarios](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

 Use the folowing sections to help you capture and restore user data.


##  <a name="BKMK_StoringUserData"></a> Store user state data  
 When you capture user state, you can store the user state data on the destination computer or on a state migration point. To store the user state on a user state migration point, you must use a Configuration Manager site system server that hosts the state migration point site system role. To store the user state on the destination computer, you must configure your task sequence to store the data locally using links.  

> [!NOTE]  
>  The links that are used to store the user state locally are referred to as hard-links. Hard-links is a USMT 10.0 feature that scans the computer for user files and settings and then creates a directory of hard-links to those files. The hard-links are then used to restore the user data after the new operating system is deployed.  

> [!IMPORTANT]  
>  You cannot use a state migration point and use hard-links to store the user state data at the same time.  

 When the user state information is captured, the information can be stored in one of the following ways:  

-   You can store the user state data remotely by configuring a state migration point. The **Capture** task sequence sends the data to the state migration point. Then, after the operating system is deployed, the **Restore** task sequence retrieves the data and restores the user state on the destination computer.  

-   You can store the user state data locally to a specific location. In this scenario, the **Capture** task sequence copies the user data to a specific location on the destination computer. Then, after the operating system is deployed, the **Restore** task sequence retrieves the user data from that location.  

-   You can specify hard links that can be used to restore the user data to its original location. In this scenario, the user state data remains on the drive when the old operating system is removed. Then, after the new operating system is deployed, the **Restore** task sequence uses the hard-links to restore the user state data to its original location.  

###  <a name="BKMK_UserDataSMP"></a> Store user data on a state migration point  
 To store the user state data on a state migration point, you must do the following:  

1.  [Configure a state migration point](#BKMK_StateMigrationPoint) to store the user state data.  

2.  [Create a computer association](#BKMK_ComputerAssociation) between the source computer and the destination computer. You must create this association before you capture the user state on the source computer.  

3.  [Create a task sequence to capture and restore user state in System Center Configuration Manager](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Specifically, you must add the following task sequence steps to capture user data from a computer, store the user date on a state migration point, and restore the user data to a computer:  

    -   [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) to request access to a state migration point when capturing state from a computer or restoring state to a computer.  

    -   [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) to capture and store the user state data on the state migration point.  

    -   [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) to restore the user state on the destination computer by retrieving the data from a user state migration point.  

    -   [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) to notify the state migration point that the capture or restore action is complete.  

###  <a name="BKMK_UserDataDestination"></a> Store user data locally  
 To store the user state data locally, you must do the following:  

-   [Create a task sequence to capture and restore user state](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Specifically, you must add the following task sequence steps to capture user data from a computer and restore the user data to a computer by using hard-links,  

    -   [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) to capture and store the user state data to a local folder by using hard-links.  

    -   [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) to restore the user state on the destination computer by retrieving the data by using hard-links.  

        > [!NOTE]  
        >  The user state data that the hard-links reference remains on the computer after the task sequence removes the old operating system. This is the data that is used to restore the user state when the new operating system is deployed.  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 The state migration point stores user state data that is captured on one computer and then restored on another computer. However, when you capture user settings for an operating system deployment on the  same computer, such as a deployment where you refresh the operating system on the destination computer, you can store the data on the same computer by using hard-links or on a state migration point. For some computer deployments, when you create the state store, Configuration Manager automatically creates an association between the state store and the destination computer. You can use the following methods to configure a state migration point to store the user state data:  

-   Use the **Create Site System Server Wizard** to create a new site system server for the state migration point.  

-   Use the **Add Site System Roles Wizard** to add a state migration point to an existing server.  

 When you use these wizards, you are prompted to provide the following information for the state migration point:  

-   The folders to store the user state data.  

-   The maximum number of clients that can store data on the state migration point.  

-   The minimum free space for the state migration point to store user state data.  

-   The deletion policy for the role. You can specify that the user state data is deleted immediately after it is restored on a computer, or after a specific number of days after the user data is restored on a computer.  

-   Whether the state migration point responds only to requests to restore user state data. When you enable this option, you cannot use the state migration point to store user state data.  

 For more information about the state migration point and the steps to configure it, see [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 Create a computer association to define a relationship between a source computer and a destination computer when you install an operating system on new hardware and want to capture and restore user data settings. The source computer is an existing computer that Configuration Manager manages. When you deploy the new operating system to the destination computer, the source computer contains the user state that is migrated to the destination computer.  

> [!NOTE]  
>  It is not supported to create a computer association between computers located in a Configuration Manager parent site with computers located in a child site. Computer Associations are site specific and do not  replicate.  

#### To create a computer association  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **User State Migration**.  

3.  On the **Home** tab, in the **Create** group, click **Create Computer Association**.  

4.  On the **Computer Association** tab of the **Computer Association Properties** dialog box, specify the source computer that has the user state to capture, and the destination computer on which to restore the user state data.  

5.  On the **User Accounts** tab, specify the user accounts to migrate to the destination computer. Specify one of the following settings:  

    -   **Capture and restore all user accounts**: This setting captures and restores all user accounts. Use this setting to create multiple associations to the same source computer.  

    -   **Capture all user accounts and restore specified accounts**: This setting captures all user accounts on the source computer and only restores the accounts that you specify on the destination computer. In addition, you can use this setting when you want to create multiple associations to the same source computer.  

    -   **Capture and restore specified user accounts**: This setting captures and restores only the accounts that you specify. You cannot create multiple associations to the same source computer when you select this setting.  

##  <a name="BKMK_MigrationFails"></a> Restore user state data when an operating system deployment fails  
 If the operating system deployment fails, use the USMT 10.0 LoadState feature to retrieve the user states data that was captured during the deployment process. This includes data that is stored on a state migration point or data that is saved locally on the destination computer. For more information on this USMT feature, see [LoadState Syntax](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx).  
