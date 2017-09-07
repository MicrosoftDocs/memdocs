---
title: Create a task sequence to capture an operating system | Microsoft Docs
description: "A build-and-capture task sequence builds a reference computer that can include specific drivers and software updates along with the operating system."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: 19
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Create a task sequence to capture an operating system in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When you use a task sequence to deploy an operating system to a computer  in System Center Configuration Manager, the  computer installs the operating system image that you specify in the task sequence. To customize the operating system image so it includes specific drivers, applications, software updates, etc., you use a build and capture task sequence to build a reference computer and then capture the operating system image from that reference computer. If you already have a reference computer available to capture, you can create a custom task sequence to capture the operating system. Use the following sections to capture a custom operating system.  

##  <a name="BKMK_BuildCaptureTS"></a> Use a task sequence to build and capture a reference computer  
 The build and capture task sequence partitions and  formats the reference computer, installs the operating system, as well as the Configuration Manager client, applications, and software updates, and then captures the operating system from the reference computer. The packages associated with the task sequence, such as applications, must be available on distribution points before you create the build and capture task sequence.  

###  <a name="BKMK_CreatePackages"></a> Prepare for operating system deployments  
 There are a lot of scenarios to deploy an operating system to computers in your environment. In most cases, you will create a task sequence  and select **Install an existing image package** in the Create Task Sequence Wizard to install the operating system, migrate user settings, apply software updates, and install applications. Before  you create a task sequence to install an operating system, the following must be in place:  

-   **Required**  

    -   The [boot image](../get-started/manage-boot-images.md) must be available in the Configuration Manager console.  

    -   An [operating system image](../get-started/manage-operating-system-images.md) must be available in the Configuration Manager console.  

-   **Required (if used)**  

    -   [Driver packages](../get-started/manage-drivers.md) that contain the necessary Windows drivers to support hardware on the reference computer must be available in the Configuration Manager console. For more information about the task sequence steps to manage drivers, see [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   [Software updates](../../sum/get-started/synchronize-software-updates.md) must be synchronized in the Configuration Manager console.  

    -   [Applications](../../apps/deploy-use/create-applications.md) must be added to the Configuration Manager console.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Create a build and capture task sequence  
 Use the following procedure to use a task sequence to  build a reference computer and capture the operating system.  

#### To create a task sequence that builds and captures an operating system image  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, select **Build and capture a reference operating system image**.  

5.  On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

    -   **Task sequence name**: Specify a name that identifies the task sequence.  

    -   **Description**: Specify a description of the task that is performed by the task sequence, such as a description of the operating system that is created by the task sequence.  

    -   **Boot image**: Specify the boot image that installs the operating system image.  

        > [!IMPORTANT]  
        >  The architecture of the boot image must be compatible with the hardware architecture of the destination computer.  

6.  On the **Install Windows** page, specify the following settings, and then click **Next**.  

    -   **Image package**: Specify the operating system image package, which contains the files that are required to install the operating system.  

    -   **Image index**: Specify the operating system to install. If the operating system image contains multiple versions, select the  version that you want to install.  

    -   **Product key**: Specify the product key for the Windows operating system to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of 5 characters must be separated by a dash (-). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Server licensing mode**: Specify that the server license is **Per seat**, **Per server**, or that no license is specified. If the server license is **Per server**, also specify the maximum number of server connections.  

    -   Specify how to handle the administrator account that is used when the operating system is deployed.  

        -   **Randomly generate the local administrator password and disable the account on all supported platforms**: Specify whether to have Configuration Manager create a random password for the local administrator account and disable the account when the operating system is deployed.  

        -   **Enable the account and specify the local administrator password**: Specify whether the same password is used for the local administrator account on all computers where the operating system is deployed.  

7.  On the **Configure Network** page, specify the following settings, and then click **Next**.  

    -   **Join a workgroup**: Specify whether to add the destination computer to a workgroup when the operating system is deployed.  

    -   **Join a domain**: Specify whether to add the destination computer to a domain when the operating system is deployed. In **Domain**, specify the name of the domain.  

        > [!IMPORTANT]  
        >  You can browse to locate domains in the local forest, but you must specify the domain name for a remote forest.  

         You can also specify an organizational unit (OU). This is an optional setting that specifies the LDAP X.500-distinguished name of the OU in which to create the computer account if it does not already exist.  

    -   **Account**: Specify the user name and password for the account that has permissions to join the specified domain. For example: *domain\user* or *%variable%*.  

        > [!IMPORTANT]  
        >  You must enter the appropriate domain credentials if you plan to migrate either the domain settings or the workgroup settings.  

8.  On the **Install Configuration Manager** page, specify the Configuration Manager client package that contains the source files to install the Configuration Manager client, add any additional properties needed to install the client, and then click **Next**.  

     For more information about properties that can be used to install a client, see [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md).  

9. On the **Include Updates** page, specify whether to install required software updates, all software updates, or no software updates, and then click **Next**. If you specify to install software updates, Configuration Manager installs only those software updates that are targeted to the collections that the destination computer is a member of.  

10. On the **Install Applications** page, specify the applications to install on the destination computer, and then click **Next**. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

11. On the **System Preparation** page, specify the following settings, and then click **Next**.  

    -   **Package**: Specify the Configuration Manager package that contains the appropriate version of Sysprep to use to capture the reference computer settings.  

         If the operating system version that you are running is Windows Vista or later, Sysprep is automatically installed on the computer and you do not have to specify a package.  

12. On the **Images Properties** page, specify the following settings for the operating system image, and then click **Next**.  

    -   **Created by**: Specify the name of the user who created the operating system image.  

    -   **Version**: Specify a user-defined version number that is associated with the operating system image.  

    -   **Description**: Specify a user-defined description of the operating system computer image.  

13. On the **Capture Image** page, specify the following settings, and then click **Next**.  

    -   **Path**: Specify a shared network folder where the output .WIM file is stored. This file contains the operating system image that is based on the settings that you specify by using this wizard. If you specify a folder that contains an existing .WIM file, the existing file is overwritten.  

    -   **Account**: Specify the Windows account that has permissions to the network share where the image is stored.  

14. Complete the wizard.  

15. To add additional steps to the task sequence, select the task sequence that you created and click **Edit**. For information about how to edit a task sequence, see [Edit a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Deploy the task sequence to a reference computer in one of the following ways:  

-   If the reference computer is a Configuration Manager client, you can deploy the build and capture task sequence to the collection that contains the reference computer. For information about how to deploy the operating system image, see [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  If the task sequence has a disk partitioning task sequence step, do not select the **Download Program** option when you deploy the task sequence.  

-   If the reference computer is not a Configuration Manager client or if you want to manually run the task sequence on the reference computer, run the **Create Task Sequence Media Wizard** to create bootable media. For information about how to create bootable media, see [Create bootable media](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Capture an operating system image from an existing reference computer  
 When you already have a reference computer ready to capture, you can create a task sequence that captures the operating system from the reference computer. You will use the **Capture Operating System Image** task sequence step to capture one or more images from a reference computer and store them in a image file (.wim) on the specified network share. The reference computer is started in Windows PE by using a boot image, each hard drive on the reference computer is captured as a separate image within the .wim file. If the referenced computer has multiple drives, the resulting .wim file will contain a separate image for each volume. Only volumes that are formatted as NTFS or FAT32 are captured. Volumes with other formats and USB volumes are skipped.  

 Use the following procedure to capture an operating system image from an existing reference computer.  

#### To capture an operating system from an existing reference computer  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, select **Create a new custom task sequence**.  

5.  On the **Task Sequence Information** page, specify a name for the task sequence and a description of the task sequence.  

6.  Specify a boot image for the task sequence. This boot image is used to start the reference computer with Windows PE.  For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

7.  Complete the wizard.  

8.  In **Task Sequences**, select the custom task sequence, and then on the **Home** tab,  in the **Task Sequence** group, click **Edit** to open the task sequence editor.  

9. Use this step only if the Configuration Manager client is installed on the reference computer.  

     Click **Add**, click **Images**, and then click [Prepare ConfigMgr Client for Capture](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). This task sequence step takes the Configuration Manager client on the reference computer and prepares it for capture as part of the imaging process.  

    > [!Note]  
    >  The task sequence does not support uninstalling the Configuration Manager client.

10. Click **Add**, click **Images**, and then click [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). This task sequence action runs Sysprep and then reboots the computer into Windows PE boot image specified for the task sequence. The reference computer must not be joined to a domain for this action to be completed successfully.  

11. Click **Add**, click **Images**, and then click [Capture Operating System Image](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  This task sequence step will only run from Windows PE to capture the hard drives on the reference computer. Configure the following settings for the task sequence step.  

    -   **Name** and **Description**: Optionally, you can change the name of the task sequence step and provide a description.  

    -   **Destination**: Specify a shared network folder where the output .WIM file is stored. This file contains the operating system image that is based on the settings that you specify by using this wizard. If you specify a folder that contains an existing .WIM file, the existing file is overwritten.  

    -   **Description**, **Version**, and **Created by**: Optionally, provide details about the image that you will capture.  

    -   **Capture operating system image account**: Specify the Windows account that has permissions to the network share you specified. Click **Set** to specify the name of that Windows account.  

     Click **OK** to close the task sequence editor.  

 Deploy the task sequence to a reference computer in one of the following ways:  

-   If the reference computer is a Configuration Manager client, you can deploy the task sequence to the collection that contains the reference computer. For information about how to deploy the operating system image, see [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md).  

-   If the reference computer is not a Configuration Manager client or if you want to manually run the task sequence on the reference computer, run the **Create Task Sequence Media Wizard** to create bootable media. For information about how to create bootable media, see [Create bootable media](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Task sequence example to build and capture an operating system image  
 Use the following table as a guide as you create a task sequence that builds and captures an operating system image. The table will help you decide the general sequence for your task sequence steps and how to organize and structure those task sequence steps into logical groups. The task sequence that you create may vary from this sample and can contain more or less task sequence steps and groups.  

> [!IMPORTANT]  
>  Always use the Create Task Sequence Wizard to create this type of task sequence.  

 When you use the **New Task Sequence** to create this new task sequence some of the task sequence step names are different than what they would be if you manually added these task sequence steps to an existing task sequence. The following table displays the naming differences:  

|New Task Sequence Wizard Task Sequence Step name|Equivalent Task Sequence Editor Step Name|  
|------------------------------------------------------|-----------------------------------------------|  
|Restart in Windows PE|Reboot to Windows PE or hard disk|  
|Partition Disk 0|Format and Partition Disk|  
|Apply Device Drivers|Auto Apply Drivers|  
|Install Updates|Install Software Updates|  
|Join Workgroup|Join Domain or Workgroup|  
|Prepare ConfigMgr Client|Prepare ConfigMgr Client for Capture|  
|Prepare Operating System|Prepare Windows for Capture|  
|Capture the Reference Machine|Capture Operating System Image|  

|Task Sequence Group/Step|Reference|  
|-------------------------------|---------------|  
|Build the Reference Computer - **(New Task Sequence Group)**|Create a task sequence group. A task sequence group keeps similar task sequence steps together for better organization and error control.<br /><br /> This group contains the actions necessary to build a reference computer.|  
|Restart in Windows PE|Use this task sequence step to specify the restart options for the destination computer. This step will display a message to the user that the computer will be restarted so that the installation can continue.<br /><br /> This step uses the read-only **_SMSTSInWinPE** task sequence variable. If the associated value equals **false** the task sequence step will continue.|  
|Partition Disk 0|Use this task sequence step to specify the actions necessary to format the hard drive on the destination computer. The default disk number is **0**.<br /><br /> This step uses the read-only **_SMSTSClientCache** task sequence variable. This step will run if the Configuration Manager client cache does not exist.|  
|Apply Operating System|Use this task sequence step to install a specified operating system image on the destination computer. This step applies all volume images contained in the WIM file to the corresponding sequential disk volume on the target computer after first deleting all files on that volume (with the exception of Configuration Manager-specific control files).|  
|Apply Windows Settings|Use this task sequence step to configure the Windows settings configuration information for the destination computer.|  
|Apply Network Settings|Use this task sequence step to specify the network or workgroup configuration information for the destination computer.|  
|Apply Device Drivers|You his task sequence step to match and install drivers as part of an operating system deployment. You can allow Windows Setup to search all existing driver categories by selecting **Consider drivers from all categories** or limit which driver categories Windows Setup searches by selecting **Limit driver matching to only consider drivers in selected categories**.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. If the associated value does not equal **FullMedia** this task sequence step will run.|  
|Setup Windows and ConfigMgr|Use this task sequence step to install the Configuration Manager client software. Configuration Manager installs and registers the Configuration Manager client GUID. You can assign the necessary installation parameters in the **Installation properties** window.|  
|Install Updates|Use this task sequence step to specify how software updates are installed on the destination computer. The destination computer is not evaluated for applicable software updates until this task sequence step runs. At that point, the destination computer is evaluated for software updates similar to any  other Configuration Manager-managed client.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. If the associated value does not equal **FullMedia** this task sequence step will run.|  
|Capture the Reference Computer - **(New Task Sequence Group)**|Create another a task sequence group. This group contains the necessary steps to prepare and capture a reference computer.|  
|Join Workgroup|Use this task sequence step to specify information needed to have the destination computer join a workgroup.|  
|Prepare ConfigMgr Client for Capture|Use this step to take the Configuration Manager client on the reference computer and prepares it for capture as part of the imaging process|  
|Prepare Operating System|Use this task sequence step to specify the Sysprep options to use when capturing Windows settings from the reference computer. This task sequence step runs Sysprep and then reboots the computer into the Windows PE boot image specified for the task sequence.|  
|Capture Operating System Image|Use this task sequence step to enter a specific existing network share and .WIM file to use when saving the image. This location is used as the package source location when adding an operating system image package using the **Add Operating System Image Package Wizard**.|  

 After you have captured an image from a reference computer, do not capture another operating system image from the reference computer because registry entries are created during the initial configuration. Create a new reference computer each time that you capture the operating system image. If you plan to use the same reference computer to create future operating system images, first uninstall the Configuration Manager client, and then reinstall the Configuration Manager client.  

## Next steps  
[Methods to deploy enterprise operating systems](methods-to-deploy-enterprise-operating-systems.md)
