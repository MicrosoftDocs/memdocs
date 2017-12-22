---
title: Create a task sequence to upgrade an operating system
titleSuffix: "Configuration Manager"
description: "Task sequences in System Center Configuration Manager can automatically upgrade an operating system from Windows 7 or later to Windows 10."
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Create a task sequence to upgrade an operating system in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use task sequences in Configuration Manager to automatically upgrade an operating system on a destination computer. This upgrade can be from Windows 7 or later to Windows 10, or from Windows Server 2012 or later to Windows Server 2016. You create a task sequence that references the operating system upgrade package and any other content to install, such as applications or software updates. The task sequence to upgrade an operating system is part of the [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md) scenario.  

##  <a name="BKMK_UpgradeOS"></a> Create a task sequence to upgrade an operating system  
 To upgrade the operating system on computers, you can create a task sequence and select **Upgrade an operating system from upgrade package** in the Create Task Sequence Wizard. The wizard adds the steps to upgrade the operating system, apply software updates, and install applications. Before you create the task sequence, the following requirements must be in place:    

-   **Required**  

     - The [operating system upgrade package](../get-started/manage-operating-system-upgrade-packages.md) must be available in the Configuration Manager console.
     - When upgrading to Windows Server 2016, select the **Ignore any dismissable compatibility messages** setting in the Upgrade Operating System task sequence step. Otherwise the upgrade will fail.

-   **Required (if used)**  

    -   [Software updates](../../sum/get-started/synchronize-software-updates.md) must be synchronized in the Configuration Manager console.  

    -   [Applications](../../apps/deploy-use/create-applications.md) must be added to the Configuration Manager console.  

#### To create a task sequence that upgrades an operating system  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, click **Upgrade an operating system from upgrade package**, and then click **Next**.  

5.  On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

    -   **Task sequence name**: Specify a name that identifies the task sequence.  

    -   **Description**: Specify a description of the task that is performed by the task sequence.  

6.  On the **Upgrade the  Windows Operating System** page, specify the following settings, and then click **Next**.  

    -   **Upgrade package**: Specify the upgrade package that contains the operating system upgrade source files. You can verify  that you have selected the correct upgrade package by looking at the information in the **Properties** pane. For more information, see [Manage operating system upgrade packages](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Edition index**: If there are multiple operating system edition indexes available in the package, select the desired edition index. By default, the first item is selected.  

    -   **Product key**: Specify the product key for the Windows operating system to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of five characters must be separated by a dash (-). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. When the upgrade is for a volume license edition, the product key is not required. You only need a product key when the upgrade is for a retail Windows edition.  

    -   **Ignore any dismissable compatibility messages**: Select this setting if you are upgrading to Windows Server 2016. If you do not select this setting, the task sequence fails to complete because Windows Setup is waiting for the user to click **Confirm** on a Windows app compatibility dialog.   

7.  On the **Include Updates** page, specify whether to install required software updates, all software updates, or no software updates, and then click **Next**. If you specify to install software updates, Configuration Manager installs only those software updates targeted to the collections of which the destination computer is a member.  

8.  On the **Install Applications** page, specify the applications to install on the destination computer, and then click **Next**. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

9. Complete the wizard.  



## Configure pre-cache content
Beginning in version 1702, the pre-cache feature for available deployments of task sequences lets clients download only relevant content before a user installs the task sequence.
> [!TIP]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.

For example, let's say you want to deploy a Windows 10 in-place upgrade task sequence, only want a single task sequence for all users, and have multiple architectures and/or languages. In previous versions, the content starts to download when the user installs an available task sequence deployment from Software Center. This delay adds additional time before the installation is ready to start. Also, all content referenced in the task sequence is downloaded. This content includes the operating system upgrade package for all languages and architectures. If each upgrade package is roughly three GB in size, the total content is very large.

Pre-cache content gives you the option to allow the client to only download the applicable content as soon as it receives the deployment. Therefore, when the user clicks **Install** in Software Center, the content is ready and the installation starts quickly because the content is on the local hard drive.

### To configure the pre-cache feature

1. Create operating system upgrade packages for specific architectures and languages. Specify the architecture and language on the **Data Source** tab of the package. For the language, use the decimal conversion (for example, 1033 is the decimal for English and 0x0409 is the hexadecimal equivalent). For details, see [Create a task sequence to upgrade an operating system](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    The architecture and language values match conditions on the steps of the task sequence to determine whether the operating system upgrade package is pre-cached.
1. Create a task sequence with conditional steps for the different languages and architectures. For example, the following step uses the English version:

    ![pre-cache properties](../media/precacheproperties2.png)

    ![pre-cache options](../media/precacheoptions2.png)  

3. Deploy the task sequence. For the pre-cache feature, configure the following settings:
    - On the **General** tab, select **Pre-download content for this task sequence**.
    - On the **Deployment settings** tab, configure the task sequence with the **Available** for **Purpose**.
    - On the **Scheduling** tab, for the **Schedule when this deployment will be available** setting, choose the currently selected time. The client starts pre-caching content at the deployment's available time. When a targeted client receives this policy, the available time is in the past, thus pre-cache download starts right away. If the client receives this policy but the available time is in the future, the client does not start pre-caching content until the available time occurs. 
    - On the **Distribution Points** tab, configure the **Deployment options** settings. If the content is not pre-cached on a client before a user starts the installation, these settings are used.


### User experience
- When the client receives the deployment policy, it will start to pre-cache the content after the deployment's available time. This content includes all referenced packages and only the operating system upgrade package that matches the client based on the conditions set in the task sequence.
- When the deployment is made available to users, a notification displays to inform users about the new deployment, and the task sequence is visible in Software Center. The user can go to Software Center and click **Install** to start the installation.
- If the content is not fully pre-cached when the user installs the task sequence, then the client uses the settings that you specify on the **Deployment Option** tab of the deployment. 



## Download Package Content task sequence step  
 The [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) step can be used before the **Upgrade Operating System** step in the following scenarios:  

-   You use a single upgrade task sequence for both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Set conditions on each step to detect the client architecture. This condition causes the step to download only the appropriate operating system upgrade package. Configure each **Download Package Content** step to use the same variable, and use the variable for the media path on the **Upgrade Operating System** step.  

-   To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Then use that variable for the **Staged content** value in the drivers section on the **Upgrade Operating System** step.  

   > [!NOTE]
   > When there is more than one package, Configuration Manager adds a numerical suffix to the variable name. For example, if you specify a variable of %mycontent% as a custom variable, this location is where the client stores all referenced content. When you refer to the variable in a subsequent step, such as **Upgrade Operating System**, use the variable with a numerical suffix. In this example, %mycontent01% or %mycontent02%, where the number corresponds to the order in which the **Download Package Content** step lists this specific content.

## Optional post-processing task sequence steps  
 After you create the task sequence, add additional steps as necessary. For example, to uninstall applications with known compatibility issues, or to add post-processing actions to run after the computer is restarted and the upgrade to Windows 10 is successful. Add these additional steps in the Post-Processing group of the task sequence.  

> [!NOTE]  
>  Because this task sequence is not linear, there are conditions on steps that can affect the results of the task sequence, depending on whether it successfully upgrades the client computer or if it has to roll back the client computer to the operating system version it started with.  

## Optional rollback task sequence steps  
 When something goes wrong with the upgrade process after the computer restarts, Windows Setup will roll back the upgrade to the previous operating system. The task sequence will then continue with any steps in the Rollback group. After you create the task sequence, you can add optional steps to the Rollback group.  

## Folder and files removed after computer restart  
 When the task sequence is complete, the client does not remove the post-processing and rollback scripts until the computer is restarted. These script files do not contain sensitive information.  
