---
title: Manage task sequences to automate tasks
titleSuffix: "Configuration Manager"
description: "You can create, edit, deploy, import, and export task sequences to manage them in your System Center Configuration Manager environment."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Manage task sequences to automate tasks in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use task sequences to automate steps in your System Center Configuration Manager environment. These steps can deploy an operating system image to a destination computer, build and capture an operating system image from a set of operating system installation files, and capture and restore user state information. Task sequences are located in the Configuration Manager console at **Software Library** > **Operating Systems** > **Task Sequence**. The **Task Sequence** node, including subfolders that you create, is replicated throughout the Configuration Manager hierarchy. For planning information, see [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md).  

 Use the following sections to manage task sequences.

##  <a name="BKMK_CreateTaskSequence"></a> Create task sequences  
 Create task sequences by using the Create Task Sequence Wizard. This wizard can create the following types of task sequences:  

|Task sequence type|More information|  
|------------------------|----------------------|  
|[Task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md)|This task sequence type creates the steps to install an operating system, as well as the option to migrate user data, include software updates, and install applications.|  
|[Task sequence to upgrade an operating system](create-a-task-sequence-to-upgrade-an-operating-system.md)|This task sequence type creates the steps to upgrade an operating system, as well as the option to include software updates and install applications.|  
|[Task sequence to capture an operating system](create-a-task-sequence-to-capture-an-operating-system.md)|This task sequence type creates the steps to build and capture an operating system from a reference computer. You can include software updates and install applications on the reference computer before the image is captured.|  
|[Task sequence to capture and restore user state](create-a-task-sequence-to-capture-and-restore-user-state.md)|This task sequence provides the steps to add to an existing task sequence to capture and restore user state data.|  
|[Task sequence to manage virtual hard disks](use-a-task-sequence-to-manage-virtual-hard-disks.md)|This task sequence type contains the steps to create a VHD, which includes to install an operating system and applications, that you can publish to System Center Virtual Machine Manager (VMM) from the Configuration Manager console.|  
|[Custom task sequence](create-a-custom-task-sequence.md)|This task sequence type does not add any steps to the task sequence. You must edit the task sequence and add steps to the task sequence after it is created.|  

## Return to previous page when a task sequence fails
Beginning in Configuration Manager version 1702, you can return to a previous page when you run a task sequence and there is a failure. Prior to this release, you had to restart the task sequence when there was a failure. For example, you can use the **Previous** button in the following scenarios:

- When a computer starts in Windows PE, the task sequence bootstrap dialog might display before the task sequence is available. When you click Next in this scenario, the final page of the task sequence displays with a message that there are no task sequences available. Now, you can click **Previous** to search again for available task sequences. You can repeat this process until the task sequence is available.
- When you run a task sequence, but dependent content packages are not yet available on distribution points, the task sequence fails. You can now distribute the missing content (if it wasn’t distributed yet) or wait for the content to be available on distribution points, and then click **Previous** to have the task sequence search again for the content.

##  <a name="BKMK_ModifyTaskSequence"></a> Edit a task sequence  
 You can modify a task sequence by adding or removing task sequence steps, adding or removing task sequence groups, or by changing the order of the steps. Use the following procedure to modify an existing task sequence.  

> [!IMPORTANT]  
>  When you edit a task sequence that was created by using the Create Task Sequence Wizard, the name of the step can be the action of the step or the type of the step. For example, you might see a step that has the name "Partition disk 0", which is the action for a step of type [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). All task sequence steps are documented by their type, not necessarily by the name of the step that is displayed in the Editor.  

#### To edit a task sequence  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  In the **Task Sequence** list, select the task sequence that you want to edit.  

4.  On the **Home** tab, in the **Task Sequence** group, click **Edit**, and then perform any of the following operations:  

    -   To add a task sequence step, click **Add**, select the type of the step, and then click the task sequence step that you want to add. For example, to add the Run Command Line step click **Add**, select **General**, and then click **Run Command Line**.  

         For a list of all task sequence steps and their type, see the table that follows this procedure.  

    -   To add a group to the task sequence, click **Add**, and then click **New Group**. After you add a group you can then add steps to the group.  

    -   To change the order of the steps and groups in the task sequence, select the step or group that you want to re-order, and then use the **Move Item Up** or **Move Item Down** icons. You can move only one step or group at a time.  

    -   To remove a step or group, select the step or group and click **Remove**.  

5.  Click **OK** to save the changes.  

 For a list of the available task sequence steps, see [Task sequence steps](../understand/task-sequence-steps.md).  

## Configure Software Center properties
Use the following procedure to configure the details for the task sequence displayed in Software Center. These details are for information only.  
1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **General** tab, the following settings for Software Center are available:
  - **Restart required**: Lets the user know whether a restart is required during the installation.
  - **Download size (MB)**: Specifies how many megabytes is displayed in Software Center for the task sequence.  
  - **Estimated run time (minutes)**: Specifies the estimated run time in minutes that's displayed in Software Center for the task sequence.

## Configure advanced task sequence settings
Use the following procedure to configure the details for the task sequence displayed in Software Center. These details are for information only.  
1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **Advanced** tab, the following settings are available:

    - **Run another program first**    
    Select this check box to run another program (in another package) before the task sequence is run. By default, this check box is cleared. The program that you specify to run first does not need to be advertised separately.

        > [!IMPORTANT]     
        This setting applies only to task sequences that run in the full operating system. Configuration Manager ignores this setting if the task sequence is started by using PXE or boot media.

    - **Package**     
        When you select **Run another program first**, enter or browse for the package that contains the program that must run before this task sequence.

    - **Program**     
    When you select **Run another program first**, select the program that must run before this task sequence from the **Program** drop-down list.

        > [!NOTE]    
        > If the selected program fails to run on a client, the task sequence will not be run. If the selected program runs successfully, it will not be run again, even if the task sequence is rerun on the same client.
 
    - **Disable this task sequence on computers where it is deployed**    
    If you select this option, all deployments that contain this task sequence are temporarily disabled. The task sequence is removed from the list of advertisements available to run and will not run until it has been re-enabled. By default, this option is cleared.

    - **Maximum allowed run time**    
    Specifies the maximum time (in minutes) that is expected to run the task sequence on the destination computer. You must use a whole number equal to or greater than zero. By default, this value is set to 120 minutes.

        > [!IMPORTANT]    
        > If you are using maintenance windows for the collection on which this task sequence is run, a conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If the maximum run time is set to **0**, the task sequence will start during the maintenance window and continue to run until it completes or fails after the maintenance window is closed. As a result, task sequences with a maximum run time set to **0** might run past the end of their maintenance windows. If you set the maximum run time to a specific period (that is, not set to **0**) that exceeds the length of any available maintenance window, then that task sequence will not be run. For more information, see [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows).
 
        If the value is set as **0**, Configuration Manager evaluates the maximum allowed run time as **12** hours (720 minutes) for monitoring progress. However, the task sequence will start as long as the countdown duration does not exceed the maintenance window value.

    > [!NOTE]    
    > If the maximum run time is reached, Configuration Manager will stop the task sequence if it is set to run with administrative rights and the allow users to interact with this program setting is not selected. If the task sequence itself is not stopped, Configuration Manager stops monitoring the task sequence after the maximum allowed run time is reached. 

    - **Use a boot image**   
        Enable this option to use the selected boot image when the task sequence is run. 

        Click **Browse** to select a different boot image. Clear this option to disable the use of the selected boot image when the task sequence is run.

    - **This task sequence can run on any platform**     
        If you select this option, Configuration Manager does not check the platform type of the destination computer when the task sequence is deployed. This option is selected by default.

    - **This task sequence can only run on the specified client platforms**    
        This option specifies the processors, operating systems, and service packs on which this task sequence can run. When you select this option, at least one platform must also be selected from the list. By default, no platforms are selected. Configuration Manager uses this information when is evaluates which destination computers in a collection receive the deployed task sequence.

        > [!NOTE]    
        > When a task sequence is run from boot media or by PXE boot, this option is ignored and the task sequence runs as though the option **This program can run on any platform** is selected.

## Configure high-impact task sequence settings
Beginning in Configuration Manager version 1702, you can set a task sequence as high-impact and customize the messages that users receive when they run the task sequence.

### Set a task sequence as a high-impact task sequence
Use the following procedure to set a task sequence as high-impact.
> [!NOTE]    
> Any task sequence that meets certain conditions is automatically defined as high-impact. For details, see [Manage high-risk deployments](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **User Notification** tab, select **This is a high-impact task sequence**.

### Create a custom notification for high-risk deployments
Use the following procedure to create a custom notification for high-impact deployments.
1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Task Sequences**.
2. Select the task sequence to edit, and click **Properties**.
3. On the **User Notification** tab, select **Use custom text**.
>  [!NOTE]    
>  You can only set user notification text when the **This is a high-impact task sequence** is selected.

4. Configure the following settings (max of 255 characters for each text box):

  **User notification headline text**: Specifies the blue text that displays on the Software Center user notification. For example, in the default user notification, this section contains something like "Confirm you want to upgrade the operating system on this computer".

  **User notification message text**: There are three text boxes that provide the body of the custom notification. All text boxes require that you add text.
  - 1st text box: Specifies the main body of text, typically containing instructions for the user. For example, in the default user notification, this section contains something like "Upgrading the operating system will take time and your computer might restart several times."
  - 2nd text box: Specifies the bold text under the main body of text. For example, in the default user notification, this section contains something like "This in-place upgrade installs the new operating system and automatically migrates your apps, data, and settings."
  - 3rd text box: Specifies the last line of text under the bold text. For example, in the default user notification, this section contains something like "Click Install to begin. Otherwise, click Cancel."   
    
Let's say you configure the following custom notification in properties.

![Custom notification for a task sequence](..\media\user-notification.png)

The following notification message will be displayed when the end-user opens the installation from Software Center.

![Custom notification for a task sequence](..\media\user-notification-enduser.png)


##  <a name="BKMK_DistributeTS"></a> Distribute content referenced by a task sequence  
 Before clients run a task sequence that references content, you must distribute that content to distribution points. At any time, you can select the task sequence and distribute its content to build a new list of reference packages for distribution. If you make changes to the task sequence with updated content, you must redistribute the content before it is available to clients. Use the following procedure to distribute the content that is referenced by a task sequence.  

#### To distribute referenced content to distribution points  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  In the **Task Sequence** list, select the task sequence that you want to distribute.  

4.  On the **Home** tab, in the **Deployment** group, click **Distribute Content** to start the Distribute Content Wizard.  

5.  On the **General** page, verify that the correct task sequence is selected for distribution, and then click **Next**.  

6.  On the **Content** page, verify the content to distribute, such as the boot image referenced by the task sequence, and then click **Next**.  

7.  On the **Content Destination** page, specify the collections, distribution point, or destination point group where you want to distribute the task sequence contents, and then click **Next**.  

    > [!IMPORTANT]  
    >  If the task sequence that you selected references content that is already distributed to a specific distribution point, that distribution point is not listed by the wizard.  

8.  Complete the wizard.  

 You can prestage the content referenced in the task sequence. Configuration Manager creates a compressed, prestaged content file that contains the files, associated dependencies, and associated metadata for the content that you select. Then, you can then manually import the content at a site server, secondary site, or distribution point. For more information about how to prestage content files, see [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

##  <a name="BKMK_DeployTS"></a> Deploy a task sequence  
 Use the following procedure to deploy a task sequence to the computers in a collection.  

> [!WARNING]  
>  You can manage the behavior for high-risk task sequence deployments. A high-risk deployment is a deployment that is automatically installed and has the potential to cause unwanted results. For example, a task sequence that has a purpose of **Required** that deploys an operating system is considered a high-risk deployment. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  The status messages for the task sequence deployment are displayed in the Message window on a primary site, but they are not displayed on a central administration site.  

#### To deploy a task sequence  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  In the **Task Sequence** list, select the task sequence that you want to deploy.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  

    > [!NOTE]  
    >  If **Deploy** is not available, the task sequence has a reference that is not valid.  Correct the reference and then try to deploy the task sequence again.  

5.  On the **General** page, specify the following information, and then click **Next**.  

    -   **Task sequence**: Specify the task sequence that you want to deploy. By default, this box displays the task sequence that you selected.  

    -   **Collection**: Specify the collection that contains the computers that will run the task sequence.  

         Do not deploy task sequences that install operating systems to inappropriate collections, such as the **All Systems** collection. Be sure that the collection that you select contains only those computers that you want to run the task sequence.  

        > [!NOTE]  
        >  When you deploy a high-risk deployment, such as an operating system, the **Select Collection** window displays only the custom collections that meet the deployment verification settings that are configured in the site's properties. High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you cannot select a built-in collection such as **All Systems**. Uncheck **Hide collections with a member count greater than the site's minimum size configuration** to see all custom collections that contain fewer clients than the configured maximum size. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  The deployment verification settings are based on the current membership of the collection. After you deploy the task sequence, the collection membership is not reevaluated for the high-risk deployment settings.  
        >   
        >  For example, let's say you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high risk deployment, the **Select Collection** window will only display collections that contain less than 100 clients. If you clear the **Hide collections with a member count greater than the site's minimum size configuration** setting, the window will display collections that contain less than 1000 clients.  
        >   
        >  When you select a collection that contains a site role, the following applies:  
        >   
        >  -   If the collection contains a site system server and in the deployment verification settings you configure to block collections with site system servers, then an error occurs and you cannot continue.  
        > -   If the collection contains a site system server and in the deployment verification settings you configure to warn you if collections that have site system servers, if the collection exceeds the default size value, or if the collection contains a server, then the Deploy Software Wizard will display a high risk warning. You must agree to create a high risk deployment and an audit status message is created.  

    -   **Comments (optional)**: Specify additional information that describes this deployment of the task sequence.  

6.  On the **Deployment Settings** page, specify the following information, and then click **Next**.  

    -   **Purpose**: From the drop-down list, choose one of the following options:  

        -   **Available**: If the task sequence is deployed to a user, the user sees the published task sequence in the Application Catalog and can request it on demand. If the task sequence is deployed to a device, the user will see it in the Software Center and can install it on demand.  

        -   **Required**: The task sequence is deployed automatically, according to the configured schedule. However, a user can track the task sequence deployment status (if it is not hidden) and install the task sequence before the deadline by using the Software Center.  

    -   **Deploy automatically according to schedule whether or not a user is logged on**: This option is not available when you deploy a task sequence.  

    -   **Send wake-up packets**: If the deployment purpose is set to **Required** and this option is selected, a wake-up packet will be sent to computers before the deployment is installed to wake the computer from sleep at the installation deadline time. Before you can use this option, computers and networks must be configured for Wake On LAN.  

    -   **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: When you have a task sequence that installs an application but does not deploy an operating system, you can specify whether to allow clients to download content after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

        > [!NOTE]  
        >  While using a metered Internet connection might work for task sequences that do not deploy an operating system, it is not supported.  

    -   **Require administrator approval if users request this application**: This option is not available when you deploy a task sequence.  

    -   **Make available to the following**: Specify whether the task sequence is available to Configuration Manager clients, media, or PXE.  

        > [!IMPORTANT]  
        >  Use the **Only media and PXE (hidden)** setting for automated task sequence deployments. Select **Allow unattended operating system deployment** and set the SMSTSPreferredAdvertID variable as part of the media to have the computer automatically boot to the deployment with no user interaction. For more information about task sequence variables, see [Task sequence built-in variables](../understand/task-sequence-built-in-variables.md)  

7.  On the **Scheduling** page, specify the following information, and then click **Next**.  

    > [!IMPORTANT]  
    >  When a Windows PE client starts from PXE or boot media, the client does not evaluate deployment schedules (start, expire, or deadline times). Only configure schedules in deployments to clients that start from the full Windows operating system. Consider using other methods, such as maintenance windows, to control active task sequences deployed to clients that start from Windows PE.  

    -   **Schedule when this deployment will become available**: Specify the date and time when the task sequence is available to run on the destination computer. When you select the **UTC** check box, this setting ensures that the task sequence is available for multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

         If the start time is earlier than the required time, the client downloads the task sequence at the start time that you specify.  

    -   **Schedule when this deployment will expire**: Specify the date and time when the task sequence expires on the destination computer. When you select the **UTC** check box, this setting ensures that the task sequence expires on multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

    -   **Assignment schedule**: Specify when the required task sequence is run on the destination computer. You can add multiple schedules.  

         You can specify the date and time when the schedule starts, whether the task sequence runs weekly, monthly, or on a custom interval, and if the task sequence runs after an event such as logging on or logging off the computer.  

        > [!NOTE]  
        >  If you schedule a start time for a required task sequence that is earlier than the date and time when the task sequence is available, the Configuration Manager client downloads the task sequence at the scheduled start time, even though the task sequence is available at an earlier time.  

    -   **Rerun behavior**: Specify when the task sequence is rerun. You can specify one of the following options.  

        -   **Never rerun deployed program**: The task sequence does not rerun on the client if the task sequence has been previously run on the client. The task sequence does not rerun even if it originally failed or if the task sequence files have been changed.  

        -   **Always rerun program**: The task sequence is always rerun on the client when the deployment is scheduled, even if the task sequence has successfully run previously. This setting is particularly useful when you use recurring deployments in which the task sequence is routinely updated.  

            > [!IMPORTANT]  
            >  Although this option is set by default, it has no affect until you assign a required deployment. Available deployments can always be rerun by a user.  

        -   **Rerun if failed previous attempt**: The task sequence is rerun when the deployment is scheduled only if the task sequence failed to run previously. This setting is particularly useful for required deployments so that they will automatically retry to run according to the assignment schedule if the last attempt to run was unsuccessful.  

        -   Rerun if succeeded on previous attempt: The task sequence is rerun only if it has previously run successfully on the client. This setting is useful when you use recurring deployments in which the task sequence is routinely updated, and each update requires that the previous update is installed successfully.  

        > [!NOTE]  
        >  Because a user can rerun an available task sequence deployment, make sure that before you deploy an available task sequence in a product environment, you carefully evaluate and test what happens if a user reruns the task sequence multiple times.  

8.  On the **User Experience** page, specify the following information, and then click **Next**.  

    -   **Allow user to run the program independently of assignments**: Specify whether the user is allowed to run a required task sequence independently from the deployment assignments.  

    -   **Show Task Sequence progress**: Specify whether the Configuration Manager client displays the progress of the task sequence.  

    -   **Software installation**: Specify whether the user is allowed to install software outside a configured maintenance windows after the scheduled time.  

    -   **System restart (if required to complete the installation)**: Specify whether the user is allowed to restart the computer after a software installation outside a configured maintenance window after the assignment time.  

    -   **Allow task sequence to run for client on the Internet**: Specify whether the task sequence is allowed to run on an Internet-based client that Configuration Manager detects to be on the Internet. Operations that install software, such as an operating system, are not supported with this setting. Use this option only for generic script-based task sequences that perform operations in the standard operating system.  

9. On the **Alerts** page, specify the alert settings that you want for this task sequence deployment, and then click **Next**.  

10. On the **Distribution Points** page, specify the following information, and then click **Next**.  

    -   **Deployment options**: Specify one of the following options:  

        > [!NOTE]  
        >  When you use multicast to deploy an operating system the content must be downloaded to the destination computers either as it is needed or before the task sequence is run.  

        -   Specify that clients download content from the distribution point to the destination computer as it is needed by the task sequence.  

        -   Specify that clients download all the content from the distribution point to the destination computer before the task sequence is run. This option is not shown if you specified that the task sequence is available to PXE and boot media deployments (see the **Deployment Settings** page).  

        -   Specify that clients run the content from the distribution point. This option is available only when all packages associated with the task sequence is enabled to use a package share on the distribution point. To enable content to use a package share, see the **Data Access** tab in the **Properties** for each package.  

    -   **When no local distribution point is available, use a remote distribution point**: Specify whether clients can use distribution points that are on slow and unreliable networks to download the content that is required by the task sequence.  

11. Complete the wizard.  

##  <a name="BKMK_ExportImport"></a> Export and import task sequences  
 You can export and import task sequences with or without their related objects, such as such an operating system image, a boot image, a client agent package, a driver package, and applications that have dependencies.  

 Consider the following when you export and import task sequences.  

-   Passwords that are stored in the task sequence are not exported. If you export and import a task sequence that contains passwords, you must edit the imported task sequence and specify any passwords again. Ensure that you specify passwords for [Join Domain or Workgroup](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Connect To Network Folder](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder), and [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) actions.  

- When you export a task sequence with the **Set Dynanmic Variables** step, no values are exported for variables that are configured with the **Secret value** setting. You must reenter the values for these variables after you import the task sequence.

-   As a best practice, when you have multiple primary sites, import task sequences at the central administration site.  

 Use the following procedures to export and import a task sequence.  

#### To export task sequences  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  In the **Task Sequence** list, select the task sequences that you want to export. If you select more than one task sequence, they are stored in one export file.  

4.  On the **Home** tab, in the **Task Sequence** group, click **Export** to start the Export Task Sequence Wizard.  

5.  On the **General** page, specify the following settings, and then click **Next**.  

    -   In the **File** box, specify the location and name of the export file. If you enter the file name directly, be sure to include the .zip extension to the file name. If you browse for the export file, the wizard automatically adds this file name extension.  

    -   Clear the **Export all task sequence dependencies** check box if you do not want to export task sequence dependencies. By default, the wizard scans for all the related objects and exports them with the task sequence. This includes any dependencies for applications.  

    -   Clear the **Export all content for the selected task sequences and dependencies** check box if you do not want to copy the content from the package source to the export location. If this check box is selected, the Import Task Sequence Wizard uses the import path as the new package source location.  

    -   In the **Administrator comments** box, add a description of the task sequences to export.  

6.  Complete the wizard.  

 The wizard creates the following output files:  

-   If you do not export content: a .zip file.  

-   If you export content: a .zip file and a folder named *export*_files, where *export* is the name of the .zip file that contains the exported content.  

 If you include content when you export a task sequence, make sure that you copy the .zip file and the *export*_files folder, or your import will fail.  

#### To import task sequences  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Import Task Sequence** to start the Import Task Sequence Wizard.  

4.  On the **General** page, specify the exported .zip file, and then click **Next**.  

5.  On the **File Content** page, select the action that you require for each object that you import. This page shows all the objects that Configuration Manager will import.  

    -   If the object has never been imported, select **Create New**.  

    -   If the object has been previously imported, select one of the following actions:  

        -   **Ignore Duplicate** (default): This action does not import the object. Instead, the wizard links the existing object to the task sequence.  

        -   **Overwrite**: This action overwrites the existing object with the imported object. For applications, you can add a revision to update the existing application or create a new application.  

6.  Complete the wizard.  

 After you import the task sequence, edit the task sequence to specify any passwords that were in the original task sequence. For security reasons, passwords are not exported.  

##  <a name="BKMK_CreateTSVariables"></a> Create task sequence variables for computers and collections  
You can define custom task sequence variables for computers and collections. Variables that are defined for a computer are referred to as per-computer task sequence variables. Variables defined for a collection are referred to as per-collection task sequence variables. If there is a conflict, per-computer variables take precedence over per-collection variables. This means that task sequence variables that are assigned to a specific computer automatically have a higher priority than variables that are assigned to the collection that contains the computer.  

For example, if collection ABC has a variable assigned to it and computer XYZ, which is a member of collection ABC, has a variable with the same name assigned to it, the variable that is assigned to computer XYZ has higher priority than that of the variable that is assigned to collection ABC.  

You can hide per-computer and per-collection variables so that they are not visible in the Configuration Manager console. If you no longer want these variables to be hidden, you must delete them and redefine them without selecting the option to hide them. When you use the option **Do not display this value in the Configuration Manager console**, the value of the variable is not displayed in the console, but can still be used by the task sequence when it runs.  

> [!WARNING]    
> The **Do not display this value in the Configuration Manager console** setting applies to the Configuration Manager console, but the values for the variables are still displayed in the task sequence log file (SMSTS.LOG). 

You can manage per-computer variables at a primary site or at a central administration site. Configuration Manager does not support more than 1,000 assigned variables for a computer.  

> [!IMPORTANT]  
>  When you use per-collection variables for task sequences, consider the following:  
>   
> - Because changes to collections are always replicated throughout the hierarchy, any changes that you make to collection variables will apply to not just members of the current site but to all members of the collection throughout the hierarchy.  
> - When you delete a collection, this action also deletes the task sequence variables that are configured for the collection.  

 Use the following procedures to create task sequence variables for a computer or collection.  

#### To create task sequence variables for a computer  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand the collection that contains the computer that you want to add the variable to.  

3.  Select the computer and click **Properties**.  

4.  In the **Properties** dialog box, click the **Variables** tab.  

5.  For each variable that you want to create, click the **New** icon in the **<New\> Variable** dialog box and specify the name and the value of the task sequence variable. Clear the **Do not display this value in the Configuration Manager console** check box if you want to hide the variables so that they are not visible in the Configuration Manager console.  

6.  After you have added all the variables to the computer, click **OK**.  

#### To create task sequence variables for a collection  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, select the collection that you want to add the variable to and click **Properties**.  

3.  In the **Properties** dialog box, click the **Collection Variables** tab.  

4.  For each variable that you want to create, click the **New** icon In the **<New\> Variable** dialog box and specify the name and the value of the task sequence variable. Clear the **Do not display this value in the Configuration Manager console** check box if you want to hide the variables so that they are not visible in the Configuration Manager console.  

5.  Optionally, specify the priority for  Configuration Manager to use when the task sequence variables are evaluated.  

6.  After you have added all the variables to the collection, click **OK**.  

## Add child task sequences to a task sequence

Beginning with Configuration Manager version 1710, you can add a new task sequence step that runs another task sequence. This creates a parent-child relationship between the task sequences. This allows you to create more modular task sequences that you can re-use.

Consider the following when you add a child task sequence to a task sequence:

 - The parent and child task sequences are effectively combined into a single policy that the client runs.
 - It is not supported to add a child task sequence that is a parent of another task sequence.
 - The environment is global. For example, if a variable is set by the parent task sequence and then changed by the child task sequence, the variable remains changed moving forward. Similarly, if the child task sequence creates a new variable, the variable is available for the remaining steps in the parent task sequence.
 - Status messages are sent per normal for a single task sequence operation.
 - The task sequences write entries to the smsts.log file, with new log entries that make it clear when a child task sequence starts.

    If the child task sequence uses steps like **Run Command Line** (without any package reference), **Format**, **BitLocker**, etc., then the task sequence will run successfully from Software Center.

### To add a child task sequence to a task sequence

1. In the task sequence editor, click **Add**, select **General**, and click **Run Task Sequence**.
2. Click **Browse** to select the child task sequence.  

##  <a name="BKMK_AdditionalActionsTS"></a> Additional actions to manage task sequences  
 You can manage task sequences by using additional actions when you select a task sequence.  

#### To select a task sequence to manage  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems,** and then click **Task Sequences**.  

3.  In the **Task Sequence** list, select the task sequence that you want to manage, and then select one of the available options.  

 Use the following table for more information about some of the additional actions to manage task sequences.  

|Action|Description|  
|------------|-----------------|  
|**Copy**|Makes a copy of the selected task sequence. You might find this action useful when you want to create a new task sequence that is based on an existing task sequence.<br /><br /> When you make a copy of a task sequence in a folder, the copy is listed in that folder until you refresh the task sequence node.  After the refresh, the copy appears in the root folder.|  
|**Disable**|Disables the task sequence so that it cannot run on computers. Disabled task sequences can be deployed to computers, but computers do not run the task sequence until it is enabled.|  
|**Enable**|Enables the task sequence so that it can be run. You do not need to redeploy a deployed task sequence after it is enabled.|  
|**Create Prestaged Content File**|Starts the Create Prestaged Content File Wizard to prestage the task sequence content. For information about how to create a prestaged content file, see [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).|  
|**Move**|Moves the selected task sequence to another folder.|  

## Next steps
[Scenarios to deploy enterprise operating systems](scenarios-to-deploy-enterprise-operating-systems.md)
