---
title: Create a task sequence to install an operating system
titleSuffix: Configuration Manager
description: Use task sequences in System Center Configuration Manager to automatically install an operating system image and other content on a destination computer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create a task sequence to install an operating system in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use task sequences in System Center Configuration Manager to automatically install an operating system image on a destination computer. You create a task sequence that references a boot image used to start the destination computer, the operating system image that you want to install on the destination computer, and any other additional content, such as other applications or software updates, that you want to install. Then you deploy the task sequence to a collection that contains the destination computer.  

##  <a name="BKMK_InstallOS"></a> Create a task sequence to install an operating system  
 There are a lot of scenarios to deploy an operating system to computers in your environment. In most cases, you will create a task sequence  and select **Install an existing image package** in the Create Task Sequence Wizard to install the operating system, migrate user settings, apply software updates, and install applications. Before  you create a task sequence to install an operating system, the following must be in place:   

-   **Required**  

    -   The [boot image](../get-started/manage-boot-images.md) must be available in the Configuration Manager console.  

    -   An [operating system image](../get-started/manage-operating-system-images.md) must be available in the Configuration Manager console.  

-   **Required (if used)**  

    -   [Software updates](../../sum/get-started/synchronize-software-updates.md) must be synchronized in the Configuration Manager console.  

    -   [Applications](../../apps/deploy-use/create-applications.md) must be added to the Configuration Manager console.  

#### To create a task sequence that installs an operating system  

1. In the Configuration Manager console, click **Software Library**.  

2. In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3. On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4. On the **Create a New Task Sequence** page, click **Install an existing Image package**, and then click **Next**.  

5. On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

   -   **Task sequence name**: Specify a name that identifies the task sequence.  

   -   **Description**: Specify a description of the task that is performed by the task sequence.  

   -   **Boot image**: Specify the boot image that installs the operating system on the destination computer. The boot image contains a contain a version of Windows PE that is used to install the operating system, as well as any additional device drivers that are required. For information, see [Manage boot images](../get-started/manage-boot-images.md).  

       > [!IMPORTANT]  
       >  The architecture of the boot image must be compatible with the hardware architecture of the destination computer.  

6. On the **Install Windows** page, specify the following settings, and then click **Next**.  

   -   **Image package**: Specify the package that contains the operating system image to install. For more information, see [Manage operating system images](../get-started/manage-operating-system-images.md).  

   -   **Image**: If the operating system image package has multiple images, specify the index of the operating system image to install.  

   -   **Partition and format the target computer installing the operating system**: Specify whether you want the task sequence to partition and format the destination computer before the operating system is installed.  

   -   **Product key**: Specify the product key for the Windows operating system to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of 5 characters must be separated by a dash (-). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

   -   **Server licensing mode**: Specify that the server license is **Per seat**, **Per server**, or that no license is specified. If the server license is **Per server**, also specify the maximum number of server connections.  

   -   Specify how to handle the administrator account that is used when the operating system image is deployed.  

       -   **Disable local administrator account**: Specify whether the local administrator account is disabled when the operating system image is deployed.  

       -   **Always use the same administrator password**: Specify whether the same password is used for the local administrator account on all computers where the operating system image is deployed.  

7. On the **Configure Network** page, specify the following settings, and then click **Next**.  

   -   **Join a workgroup**: Specify whether to add the destination computer to a workgroup.  

   -   **Join a domain**: Specify whether to add the destination computer to a domain. In **Domain**, specify the name of the domain.  

       > [!IMPORTANT]  
       >  You can browse to locate domains in the local forest, but you must specify the domain name for a remote forest.  

        You can also specify an organizational unit (OU). This is an optional setting that specifies the LDAP X.500-distinguished name of the OU in which to create the computer account if it does not already exist.  

   -   **Account**: Specify the user name and password for the account that has permissions to join the specified domain. For example: *domain\user* or *%variable%*.  

       > [!IMPORTANT]  
       >  You must enter the appropriate domain credentials if you plan to migrate either the domain settings or the workgroup settings.  

8. On the **Install Configuration Manager** page, specify the Configuration Manager client package to install on the destination computer, and then click **Next**.  

9. On the **State Migration** page, specify the following information, and then click **Next**.  

    -   **Capture user settings**: Specify whether the task sequence captures the user state. For more information about how to capture and restore the user state, see [Manage user state](../get-started/manage-user-state.md).  

    -   **Capture network settings**: Specify whether the task sequence captures network settings from the destination computer. You can capture the membership of the domain or workgroup in addition to the network adapter settings.  

    -   **Capture Microsoft Windows settings**:  Specify whether the task sequence captures Windows settings from the destination computer before the operating system image is installed. You can capture the computer name, registered user and organization name, and the time zone settings.  

10. On the **Include Updates** page, specify whether to install required software updates, all software updates, or no software updates, and then click **Next**. If you specify to install software updates, Configuration Manager installs only those software updates that are targeted to the collections that the destination computer is a member of.  

11. On the **Install Applications** page, specify the applications to install on the destination computer, and then click **Next**. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

12. Complete the wizard.  

    You can now deploy the task sequence to a collection of computers.  For more information, see [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Example task sequence to install an existing operating system image  
 Use the following table as a guide as you create a task sequence that deploys an operating system using an existing operating system image. The table will help you decide the general sequence for your task sequence steps and how to organize and structure those task sequence steps into logical groups. The task sequence that you create may vary from this sample and can contain more or less task sequence steps and groups.  

> [!IMPORTANT]  
>  You must always use the Create Task Sequence Wizard to create this task sequence.  

 When you use the Create Task Sequence Wizard to create this new task sequence some of the task sequence step names are different than what than what they would be if you manually added these task sequence steps to an existing task sequence. The following table displays the naming differences:  

|Create Task Sequence Wizard Task Sequence Step name|Equivalent Task Sequence Editor Step Name|  
|---------------------------------------------------------|-----------------------------------------------|  
|Request User State Storage|Request State Store|  
|Capture User Files and Settings|Capture User State|  
|Release User State Storage|Release State Store|  
|Restart in Windows PE|Reboot to Windows PE or hard disk|  
|Partition Disk 0|Format and Partition Disk|  
|Restore User Files and Settings|Restore User State|  

|Task Sequence Group or Step|Description|  
|---------------------------------|-----------------|  
|Capture File and Settings - **(New Task Sequence Group)**|Create a task sequence group. A task sequence group keeps similar task sequence steps together for better organization and error control.<br /><br /> This group contains the steps needed to capture files and settings from the operating system of a reference computer.|  
|Capture Windows Settings|Use this task sequence step to identify the Microsoft Windows settings to capture from the reference computer. You can capture the computer name, user and organizational information and the time zone settings.|  
|Capture Network Settings|Use this task sequence step to capture network settings from the reference computer. You can capture the domain or workgroup membership of the reference computer and the network adapter setting information.|  
|Capture User Files and Settings - **(New Task Sequence Sub-Group)**|Create a task sequence group within a task sequence group. This sub-group contains the steps needed to capture user state data. Similar to the initial group that you added, this sub-group keeps similar task sequence steps together for better organization and error control.|  
|Request User State Storage|Use this task sequence step to request access to a state migration point where the user state data is stored. You can configure this task sequence step to capture or restore the user state information.|  
|Capture User Files and Settings|Use this task sequence step to use the User State Migration Tool (USMT) to capture the user state and settings from the reference computer that will receive the task sequence associated with this task step. You can capture the standard options or configure whish options to capture.|  
|Release User State Storage|Use this task sequence step to notify the state migration point that the capture or restore action is complete.|  
|Install Operating System - **(New Task Sequence Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to install and configure the Windows PE environment.|  
|Restart in Windows PE|Use this task sequence step to specify the restart options for the destination computer that receives this task sequence. This step will display a message to the user indicating that the computer will be restarted so that the installation can continue.<br /><br /> This step uses the read-only **_SMSTSInWinPE** task sequence variable. If the associated value equals **false** the task sequence step continues.|  
|Partition Disk 0|This task sequence step specifies the actions necessary to format the hard drive on the destination computer. The default disk number is **0**.<br /><br /> This step uses the read-only **_SMSTSClientCache** task sequence variable. This step will run if the Configuration Manager client cache does not exist.|  
|Apply Operating System|Use this task sequence step to install the  operating system image onto the destination computer. This step applies all volume images contained in the WIM file to the corresponding sequential disk volume on the target computer after first deleting all files on that volume (with the exception of Configuration Manager-specific control files). You can specify a **sysprep** answer file and also configure which disk partition is used for the installation.|  
|Apply Windows Settings|Use this task sequence step to configure the Windows settings configuration information for the destination computer. The windows settings you can apply are user and organizational information, product or license key information, time zone, and the local administrator password.|  
|Apply Network Settings|Use this task sequence step to specify the network or workgroup configuration information for the destination computer. You can also specify if the computer uses a DHCP server or you can statically assign the IP address information.|  
|Apply Device Drivers|Use this task sequence step to  install drivers as part of the operating system deployment. You can allow Windows Setup to search all existing driver categories by selecting **Consider drivers from all categories** or limit which driver categories Windows Setup searches by selecting **Limit driver matching to only consider drivers in selected categories**.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. This task sequence step runs only if the value of the variable does not equal **FullMedia**.|  
|Apply Driver Package|Use this task sequence step to make all device drivers in a driver package available for use by Windows setup.|  
|Setup Operating System - **(New Task Sequence Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to set up the installed operating system.|  
|Setup Windows and ConfigMgr|Use this task sequence step to install the Configuration Manager client software. Configuration Manager installs and registers the Configuration Manager client GUID. You can assign the necessary installation parameters in the **Installation properties** window.|  
|Install Updates|Use this task sequence step to specify how software updates are installed on the destination computer. The destination computer is not evaluated for applicable software updates until this task sequence step runs. At that point, the destination computer is evaluated for software updates similar to any other Configuration Manager-managed client.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. This task sequence step runs only if the value of the variable does not equal **FullMedia**.|  
|Restore User Files and Settings - **(New Task Sequence Sub-Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to restore the user files and settings.|  
|Request User State Storage|Use this task sequence step to request access to a state migration point where the user state data is stored.|  
|Restore User Files and Settings|Use this task sequence step to initiate the User State Migration Tool (USMT) to restore user state and settings to a destination computer.|  
|Release User State Storage|Use this task sequence step to notify the state migration point that the user state data is no longer needed.|  
