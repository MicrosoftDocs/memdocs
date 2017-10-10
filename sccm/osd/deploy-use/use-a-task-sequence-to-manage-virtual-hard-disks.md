---
title: Use a task sequence to manage virtual hard disks
titleSuffix: "Configuration Manager"
description: "Create and modify a VHD, add applications and software updates, and publish the VHD to System Center Virtual Machine Manager (VMM) from Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: 5
author: Dougebyms.author: dougebymanager: angrobe

---
# Use a task sequence to manage virtual hard disks in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In System Center Configuration Manager, you can manage virtual hard disks (VHDs) and integrate the VHDs that you create into your datacenter from the Configuration Manager console. Specifically, you can create and modify a VHD, add applications and software updates to the VHD, and publish the VHD to System Center Virtual Machine Manager (VMM) from the Configuration Manager console.  

 Use the following sections to manage VHDs in Configuration Manager.

## Prerequisites  
 Verify the following prerequisites before you begin:  

-   The computer from which you manage VHDs must run one of the following operating systems:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   Virtualization must be enabled in the BIOS and Hyper-V must be installed on the computer from which you run the Configuration Manager console to manage VHDs. Also as a best practice, install the Hyper-V management tools to help you test and troubleshoot your virtual hard disks. For example, to monitor the smsts.log file to track the progress of the task sequence in Hyper-V you must have the Hyper-V management tools installed. For more information about Hyper-V requirements, see [Hyper-V Installation Prerequisites](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  The process to create a VHD consumes processor time and memory. Therefore, it is recommended that you manage VHDs from a Configuration Manager console that is not installed on the site server.  

-   The site server must have **Write** access permission to the folder that will contain the VHD file when you manage VHDs from a computer that is remote from the site server.  

-   Verify that you have enough free disk space on the computer from which you manage the VHDs. The hard disk space requirements of the VHD will vary depending on the operating system and applications that you install.  

-   Verify that you have enough memory on the computer from which you manage the VHDs. During the process to create the VHD, the virtual machine is configured to consume 2 GB of memory.  

-   Install the System Center Virtual Machine Manager (VMM) console on the computer from which you upload the VHD to VMM. You can install the VMM console on a separate computer from which you manage your VHDs, which means you do not need to have Hyper-V installed to import the VHD to VMM.  

    > [!NOTE]  
    >  If you install the VMM console while the Configuration Manager console is open, you must restart the Configuration Manager console after the VMM console installation completes. Otherwise, Configuration Manager will not successfully connect to the VMM management server to upload a VHD.  

##  <a name="BKMK_CreateVHDSteps"></a> Steps to Create a VHD  
 To create a VHD, you must create a task sequence that contains the steps to create the VHD, and then use the task sequence in the Create Virtual Hard Drive Wizard to create the VHD. The following sections provide the steps to create the VHD.  

###  <a name="BKMK_CreateTS"></a> Create a Task Sequence for the VHD  
 You must create a task sequence that will contain the steps to create the VHD. In the Create Task Sequence Wizard, you have the **Install an existing image package to a virtual hard disk** option that creates the steps to use to create the VHD. For example, the wizard adds the following required steps: Restart in Windows PE, Format and Partition Disk, Apply Operating System, and Shutdown Computer. You cannot create the VHD while in the full operating system. Also, Configuration Manager must wait until the virtual machine is shut down before it can complete the package. By default, the wizard waits for 5 minutes before it shuts down the virtual machine. After you create the task sequence you can add additional steps if necessary.  

> [!IMPORTANT]  
>  The following procedure creates the task sequence by using the **Install an existing image package to a virtual hard disk** option, which automatically includes the required steps to successfully create the VHD. If you choose to use an existing task sequence or manually create a task sequence, be sure that you add the Shutdown Computer step at the end of the task sequence. Without this step, the temporary virtual machine is not deleted and process to create the VHD does not complete. However, the wizard completes and reports success.  

 Use the following procedure to create the task sequence to create the VHD:  

#### To create the task sequence to create the VHD  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, click **Install an existing image package to a virtual hard disk**, and then click **Next**.  

5.  On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

    -   **Task sequence name**: Specify a name that identifies the task sequence.  

    -   **Description**: Specify a description of the task sequence.  

    -   **Boot image**: Specify the boot image that installs the operating system on the destination computer. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

6.  On the **Install Windows** page, specify the following settings, and then click **Next**.  

    -   **Image package**: Specify the package that contains the operating system image to install.  

    -   **Image**: If the operating system image package has multiple images, specify the index of the operating system image to install.  

    -   **Product key**: Specify the product key for the Windows operating system to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of 5 characters must be separated by a dash (-). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Server licensing mode**: Specify that the server license is **Per seat**, **Per server**, or that no license is specified. If the server license is **Per server**, also specify the maximum number of server connections.  

    -   Specify how to handle the administrator account that is used when the operating system image is deployed.  

        -   **Randomly generate the local administrator password and disable the account on all supported platforms (recommended)**: Use this setting to have the wizard randomly create a password for the local administrator account and disable the account when the operating system image is deployed.  

        -   **Enable the account and specify the local administrator password**: Use this setting to use a specific password for the local administrator account on all computers where the operating system image is deployed.  

7.  On the **Configure Network** page, specify the following settings, and then click **Next**.  

    -   **Join a workgroup**: Specify whether to add the destination computer to a workgroup.  

    -   **Join a domain**: Specify whether to add the destination computer to a domain. In **Domain**, specify the name of the domain.  

        > [!IMPORTANT]  
        >  You can browse to locate domains in the local forest, but you must specify the domain name for a remote forest.  

         You can also specify an organizational unit (OU). This is an optional setting that specifies the LDAP X.500-distinguished name of the OU in which to create the computer account if it does not already exist.  

    -   **Account**: Specify the user name and password for the account that has permissions to join the specified domain. For example: *domain\user* or *%variable%*.  

8.  On the **Install Configuration Manager** page, specify the Configuration Manager client package to install on the destination computer, and then click **Next**.  

9. On the **Install Applications** page, specify the applications to install on the destination computer, and then click **Next**. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

10. Complete the wizard.  

###  <a name="BKMK_CreateVHD"></a> Create a VHD  
 After you create a task sequence for the VHD, use the Create Virtual Hard Disk Wizard to create the VHD.  

> [!IMPORTANT]  
>  Before you run this procedure, verify that you meet the prerequisites listed at the start of this topic.  

 Use the following procedure to create a VHD.  

#### To create a VHD  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Virtual Hard Disks**.  

3.  On the **Home** tab, in the **Create** group, click **Create Virtual Hard Disk** to start the Create Virtual Hard Disk Wizard.  

    > [!NOTE]  
    >  Hyper-V must be installed on the computer running the Configuration Manager console from which you manage VHDs or the **Create Virtual Hard Disk** option is not enabled. For more information about Hyper-V requirements, see [Hyper-V Installation Prerequisites](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  To organize your VHDs, create a new folder or select an existing folder under the **Virtual Hard Disks** node, and then click **Create Virtual Hard Disk** from the folder.  

4.  On the **General** page, specify the following settings, and then click **Next**.  

    -   **Name**: Specify a unique name for the VHD.  

    -   **Version**: Specify a version number for the VHD. This is an optional setting.  

    -   **Comment**: Specify a description for the VHD.  

    -   **Path**: Specify the path and file name for where the wizard will create the VHD file.  

         You must enter a valid network path in the UNC format. For example: **\\\servername\\<sharename\>\\<filename\>.vhd**.  

        > [!WARNING]  
        >  Configuration Manager must have **Write** access permission to the specified path to create the VHD. When Configuration Manager fails to access the path, it logs the associated error in the distmgr.log file on the site server.  

5.  On the **Task Sequence** page, specify the task sequence that you specified in the previous section, and then click **Next**.  

6.  On the **Distribution Points** page, select one or more distribution points that contain the content required by the task sequence, and then click **Next**.  

7.  On the **Customization** page, click **Next**. The process to create the VHD ignores any settings that you specify on this page.  

8.  Verify the settings and then click **Next**. The wizard creates the VHD.  

    > [!TIP]  
    >  The time to complete the process to create the VHD can vary. While the wizard works through this process, you can monitor the following log files to track the progress. By default, the logs are located on the computer running the Configuration Manager console at %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: The wizard writes information to this log while it creates the task sequence media. Review this log file to track the progress of the wizard when it creates the standalone media.  
    > -   **DeployToVHD.log**: The wizard writes information to this log while it goes through the process to create the VHD. Review this log file to track the progress of the wizard for all steps after it creates the standalone media.  
    >   
    >  Also, when the operating system installation starts, you can open Hyper-V Manager (if you installed the Hyper-V management tools on the computer) and connect to the temporary virtual machine created by the wizard to see the task sequence running. From the virtual machine, you can monitor the smsts.log file to track the progress of the task sequence. When there are issues with completing a task sequence step, you can use this log file to help you troubleshoot the issue. The smsts.log file is in x: \windows\temp\smstslog\smsts.log before the hard disk if formatted and in c:\\_SMSTaskSequence\Logs\Smstslog\ after it is formatted. After the task sequence steps complete, the virtual machine is shut down after 5 minutes (by default) and deleted.  

 After Configuration Manager creates the VHD, it is located in the **Virtual Hard Drives** node in the Configuration Manager console under the **Operating System Deployment** node in the **Software Library** workspace.  

> [!NOTE]  
>  Configuration Manager retrieves the size of the VHD by connecting to the source location of the VHD. If Configuration Manager cannot access the VHD file, **0** is displayed in the **Size (KB)** column for the VHD.  

##  <a name="BKMK_ModifyVHDSteps"></a> Steps to Modify an Existing VHD  
 To modify a VHD, you must create a task sequence with the steps required to modify the VHD. Then, select the task sequence in the Modify Virtual Hard Drive Wizard. The wizard attaches the VHD to the virtual machine, runs the task sequence in the VHD, and then updates the VHD file. The following sections provide the steps to modify the VHD.  

###  <a name="BKMK_ModifyTS"></a> Create a Task Sequence to Modify the VHD  
 To modify an existing VHD, you must first create a task sequence. Choose only the steps that are required to modify the task sequence. For example, if you want to add an application to the VHD, create a custom task sequence, and then add only the Install Application step.  

 Use the following procedure to create the task sequence to modify the VHD.  

#### To create a custom task sequence to modify the VHD  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, select **Create a new custom task sequence**, and then click **Next**.  

5.  On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

    -   **Task sequence name**: Specify a name that identifies the task sequence.  

    -   **Description**: Specify a description of the task sequence.  

    -   **Boot image**: Specify the boot image that installs the operating system on the destination computer. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

6.  Complete the wizard.  

 Use the following procedure to add task sequence steps to the custom task sequence.  

#### To add task sequence steps to the custom task sequence  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, click **Task Sequences**, and then select the custom task sequence that you created in the previous procedure.  

3.  On the **Home** tab, in the **Task Sequence** group, click **Edit** to start the task sequence editor.  

4.  Add the task sequence steps to use to modify the VHD.  

5.  Click **OK** to exit the task sequence editor.  

###  <a name="BKMK_ModifyVHD"></a> Modify a VHD  
 After you create a task sequence for the VHD, use the Modify Virtual Hard Disk Wizard to modify the VHD.  

 Use the following procedure to modify a VHD.  

#### To modify a VHD  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, click **Virtual Hard Disks**, and then select the VHD to modify.  

3.  On the **Home** tab, in the **Virtual Hard Disk** group, click **Modify Virtual Hard Disk** to start the Modify Virtual Hard Disk Wizard.  

    > [!NOTE]  
    >  Hyper-V must be installed on the computer running the Configuration Manager console from which you manage VHDs or the **Modify Virtual Hard Disk** option is not enabled. For more information about Hyper-V requirements, see [Hyper-V Installation Prerequisites](http://technet.microsoft.com/library/cc731898.aspx).  

4.  On the **General** page, confirm the following settings, and then click **Next**.  

    -   **Name**: Specifies the unique name for the VHD.  

    -   **Version**: Specifies the version number for the VHD. This is an optional setting.  

    -   **Comment**: Specifies the description for the VHD.  

    -   **Path**: Specifies the path and file name for where the VHD file is located. You cannot modify this setting.  

        > [!WARNING]  
        >  Configuration Manager must have **Write** access permission to the specified path to create the VHD. When Configuration Manager fails to access the path, it logs the associated error in the distmgr.log file on the site server.  

5.  On the **Task Sequence** page, specify the custom task sequence that you created in the previous section, and then click **Next**.  

6.  On the **Distribution Points** page, select one or more distribution points that contain the content required by the task sequence, and then click **Next**.  

7.  On the **Customization** page, click **Next**. The process to modify the VHD ignores any settings that you specify on this page.  

8.  Verify the settings and then click **Next**. The wizard creates the modified VHD.  

    > [!TIP]  
    >  The time to complete the process to modify the VHD can vary. While the wizard works through this process, you can monitor the following log files to track the progress. By default, the logs are located on the computer running the Configuration Manager console at %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: The wizard writes information to this log while it creates the task sequence media. Review this log file to track the progress of the wizard when it creates the standalone media.  
    > -   **DeployToVHD.log**: The wizard writes information to this log while it goes through the process to modify the VHD. Review this log file to track the progress of the wizard for all steps after it creates the standalone media.  
    >   
    >  Also, you can open Hyper-V Manager (if you installed the Hyper-V management tools on the computer) and connect to the temporary virtual machine created by the wizard to see the task sequence running. From the virtual machine, you can monitor the smsts.log file to track the progress of the task sequence. When there are issues with completing a task sequence step, you can use this log file to help you troubleshoot the issue. The smsts.log file is in x: \windows\temp\smstslog\smsts.log before the hard disk if formatted and in c:\\_SMSTaskSequence\Logs\Smstslog\ after it is formatted. After the task sequence steps complete, the virtual machine is shut down after 5 minutes (by default) and deleted.  

##  <a name="BKMK_ApplyUpdates"></a> Apply Software Updates to a VHD  
 Periodically, new software updates are released that are applicable to the operating system in your VHD. You can apply applicable software updates to a VHD on a specified schedule. On the schedule that you specify, Configuration Manager applies the software updates that you select to the VHD.  

 Information about the VHD is stored in the site database, including the software updates that were applied at the time you created the VHD. Software updates that have been applied to the VHD since it was initially created are also stored in the site database. When you start the wizard to apply software updates to the VHD, the wizard retrieves a list of applicable software updates that have not yet been applied to the VHD for you to select.  

 You can select the **Continue on error** setting for Configuration Manager to continue to apply software updates even when there is an error applying one or more of the software updates that you selected.  

> [!NOTE]  
>  The software updates are copied from the content library on the site server.  

 Use the following procedure to apply software updates to VHD.  

#### To apply software updates to a VHD  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Virtual Hard Disks**.  

3.  Select the VHD to apply software updates.  

4.  On the **Home** tab, in the **Virtual Hard Disk** group, click **Schedule Updates** to start the wizard.  

5.  On the **Choose Updates** page, select the software updates to apply to the VHD, and then click **Next**.  

6.  On the **Set Schedule** page, specify the following settings, and then click **Next**.  

    1.  **Schedule**: Specify the schedule for when the software updates are applied to the VHD.  

    2.  **Continue on error**: Select this option to continue to apply software updates to the image even when there is an error.  

7.  On the **Summary** page, verify the information, and then click **Next**.  

8.  On the **Completion** page, verify that the software updates were successfully applied to the operating system image.  

##  <a name="BKMK_ImportToVMM"></a> Import the VHD to System Center Virtual Machine Manager  
 System Center VMM is a management solution for the virtualized datacenter, enabling you to configure and manage your virtualization host, networking, and storage resources in order to create and deploy virtual machines and services to private clouds that you have created. After you create a VHD in Configuration Manager, you can import and manage your VHD by using VMM.  

> [!TIP]  
>  Before you upload a VHD to VMM, verify that the VMM console successfully connects to the VMM management server.  

 Use the following procedure to import a VHD to VMM.  

#### To import a VHD to VMM  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Virtual Hard Disks**.  

3.  On the **Home** tab, in the **Virtual Hard Disk** group, click **Upload to Virtual Machine Manager** to start the Upload to Virtual Machine Manager Wizard.  

4.  On the **General** page, configure the following settings, and then click **Next**.  

    -   **VMM server name**: Specify the FQDN of the computer on which the VMM management server is installed. The wizard connects to the VMM management server to download the library shares for the server.  

    -   **VMM library share**: Specify the VMM library share from the drop-down list.  

    -   **Use unencrypted transfer**: Select this setting to transfer the VHD file to the VMM management server without the use of encryption.  

5.  On the Summary page, verify the settings, and then complete the wizard. The time it takes to upload the VHD can vary depending on the size of the VHD file and the network bandwidth to the VMM management server.  
