---
title: Create a task sequence to install an OS
titleSuffix: Configuration Manager
description: Use task sequences in Configuration Manager to automatically install an OS image and other content on a destination computer.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create a task sequence to install an OS

*Applies to: Configuration Manager (current branch)*

Use task sequences in Configuration Manager to automatically install an OS image on a destination computer. You create a task sequence that references a boot image used to start the destination computer, the OS image that you want to install on the destination computer, and any other additional content, such as other applications or software updates, that you want to install. Then you deploy the task sequence to a collection that contains the destination computer.  

## <a name="BKMK_InstallOS"></a> Create a task sequence to install an OS

There are multiple scenarios to deploy an OS to computers in your environment. In most cases, create a task sequence and select **Install an existing image package** in the Create Task Sequence Wizard. This option creates a task sequence that installs the OS, migrates user settings, applies software updates, and installs applications.

### Prerequisites

Before you create a task sequence to install an OS, the following requirements must be in place:

#### Required

- A [boot image](../get-started/manage-boot-images.md)  

- An [OS image](../get-started/manage-operating-system-images.md)  

#### Required (if used)

- Synchronize [software updates](../../sum/get-started/synchronize-software-updates.md)  

- Add [applications](../../apps/deploy-use/create-applications.md)  

### Process to create a task sequence that installs an OS  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence**. This action starts the Create Task Sequence Wizard.  

3. On the **Create a New Task Sequence** page, select **Install an existing Image package**, and then select **Next**.  

4. On the **Task Sequence Information** page, specify the following settings:  

    - **Task sequence name**: Specify a name that identifies the task sequence.  

    - **Description**: Specify a description of what the task sequence does.  

    - **Boot image**: Specify the boot image that the task sequence uses to install the OS on the destination computer. The boot image contains a version of Windows PE, plus any additional required device drivers. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > The architecture of the boot image must be compatible with the hardware architecture of the destination computer.  

5. On the **Install Windows** page, specify the following settings:  

    - **Image package**: Specify the package that contains the OS image to install. For more information, see [Manage OS images](../get-started/manage-operating-system-images.md).  

    - **Image**: If the OS image package has multiple images, specify the index of the OS image to install.  

    - **Partition and format the target computer installing the operating system**: Specify whether you want the task sequence to partition and format the destination computer before it installs the OS.  

    - **Product key**: Specify the Windows product key, if necessary. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of five characters must be separated by a dash (`-`). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Server licensing mode**: Specify that the server license is **Per seat**, **Per server**, or that no license is specified. If the server license is **Per server**, also specify the maximum number of server connections.  

    - Specify how to handle the administrator account for the new OS:  

        - **Randomly generate the local administrator account password and disable the account on all supported platform (recommended)**: Windows disables the local administrator account after the task sequence deploys the OS image.  

        - **Enable the account and specify the local administrator password**: Windows uses the same password for the local administrator account on all computers where the task sequence deploys the OS image.  

6. On the **Configure Network** page, specify the following settings:  

    - **Join a workgroup**: Add the destination computer to a workgroup.  

    - **Join a domain**: Add the destination computer to a domain. In **Domain**, specify the name of the domain.  

        > [!IMPORTANT]  
        > You can browse to locate domains in the local forest, but you must specify the domain name for a remote forest.  

        You can also specify an organizational unit (OU) in the **Domain OU** field. This setting is optional, and specifies the LDAP X.500-distinguished name of the OU. If it doesn't already exist, Windows creates the computer account in this OU.  

    - **Account**: The user name and password for the account that has permissions to join the specified domain. For example: *domain\user* or *%variable%*.  

        > [!IMPORTANT]  
        > If you plan to migrate either the domain settings or the workgroup settings, enter the appropriate domain credentials.  

7. On the **Install Configuration Manager** page, specify the Configuration Manager client package to install on the destination computer. You can also include any installation properties.  

8. On the **State Migration** page, specify the following information:  

    - **Capture user settings**: The task sequence captures the user state. For more information about how to capture and restore the user state, see [Manage user state](../get-started/manage-user-state.md).  

    - **Capture network settings**: The task sequence captures network settings from the destination computer. It captures the membership of the domain or workgroup, also the network adapter settings.  

    - **Capture Microsoft Windows settings**: The task sequence captures Windows settings from the destination computer before it installs the OS image. It captures the computer name, registered user and organization name, and the time zone settings.  

9. On the **Include Updates** page, specify whether to install required software updates, all software updates, or no software updates. If you specify to install software updates, Configuration Manager installs only those software updates that are targeted to the collections that the destination computer is a member of.  

10. On the **Install Applications** page, specify the applications to install on the destination computer. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

11. Complete the wizard.  

You can now deploy the task sequence to a collection of computers. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).


## Pre-cache content

<!--4224642-->
Starting in version 1906, you can enable this type of task sequence to pre-cache content. The pre-cache feature for available deployments of task sequences lets clients download relevant content before a user installs the task sequence.  

For more information, see [Configure pre-cache content](configure-precache-content.md).


## <a name="BKMK_InstallExistingOSImageTSExample"></a> Example task sequence

Use the following table as a guide as you create a task sequence that deploys an OS using an existing image. The table helps you decide the general sequence for your task sequence steps and how to organize and structure those task sequence steps into logical groups. The task sequence that you create may vary from this sample and can contain more or less task sequence steps and groups.  

> [!NOTE]  
> Use the Create Task Sequence Wizard to create this task sequence.  
>
> When you use the Create Task Sequence Wizard to create this new task sequence, some of the step names are different than what they would be if you manually added these task sequence steps to an existing task sequence.

|Task sequence group or step|Description|  
|---------------------------------|-----------------|  
|Capture File and Settings - **(New task sequence group)**|Create a task sequence group. A task sequence group keeps similar task sequence steps together for better organization and error control.<br /><br /> This group contains the steps needed to capture files and settings from the operating system of a reference computer.|  
|Capture Windows Settings|Use this task sequence step to identify the Microsoft Windows settings to capture from the reference computer. You can capture the computer name, user and organizational information, and the time zone settings.|  
|Capture Network Settings|Use this task sequence step to capture network settings from the reference computer. You can capture the domain or workgroup membership of the reference computer and the network adapter setting information.|  
|Capture User Files and Settings - **(New task sequence subgroup)**|Create a task sequence group within a task sequence group. This subgroup contains the steps needed to capture user state data. Similar to the initial group that you added, this subgroup keeps similar task sequence steps together for better organization and error control.|  
|Request User State Storage|Use this task sequence step to request access to a state migration point where the user state data is stored. You can configure this task sequence step to capture or restore the user state information.|  
|Capture User Files and Settings|Use this task sequence step to use the User State Migration Tool (USMT) to capture the user state and settings from the reference computer that will receive the task sequence associated with this task step. You can capture the standard options or configure which options to capture.|  
|Release User State Storage|Use this task sequence step to notify the state migration point that the capture or restore action is complete.|  
|Install Operating System - **(New task sequence group)**|Create another task sequence subgroup. This subgroup contains the steps needed to install and configure the Windows PE environment.|  
|Restart in Windows PE|Use this task sequence step to specify the restart options for the destination computer that receives this task sequence. This step will display a message to the user indicating that the computer will be restarted so that the installation can continue.<br /><br /> This step uses the read-only **_SMSTSInWinPE** task sequence variable. If the associated value equals **false** the task sequence step continues.|  
|Partition Disk 0|This task sequence step specifies the actions necessary to format the hard drive on the destination computer. The default disk number is **0**.<br /><br /> This step uses the read-only **_SMSTSClientCache** task sequence variable. This step runs if the Configuration Manager client cache doesn't exist.|  
|Apply Operating System|Use this task sequence step to install the  operating system image onto the destination computer. This step first deletes all files on the volume, except for any Configuration Manager-specific control files. It then applies all volume images contained in the WIM file to the corresponding sequential disk volume on the target computer. You can specify a **sysprep** answer file and also configure which disk partition is used for the installation.|  
|Apply Windows Settings|Use this task sequence step to configure the Windows settings configuration information for the destination computer. The windows settings you can apply are user and organizational information, product or license key information, time zone, and the local administrator password.|  
|Apply Network Settings|Use this task sequence step to specify the network or workgroup configuration information for the destination computer. You can also specify if the computer uses a DHCP server or you can statically assign the IP address information.|  
|Apply Device Drivers|Use this task sequence step to  install drivers as part of the operating system deployment. You can allow Windows Setup to search all existing driver categories by selecting **Consider drivers from all categories** or limit which driver categories Windows Setup searches by selecting **Limit driver matching to only consider drivers in selected categories**.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. This task sequence step runs only if the value of the variable doesn't equal **FullMedia**.|  
|Apply Driver Package|Use this task sequence step to make all device drivers in a driver package available for use by Windows setup.|  
|Setup Operating System - **(New task sequence group)**|Create another task sequence subgroup. This subgroup contains the steps needed to set up the installed operating system.|  
|Setup Windows and ConfigMgr|Use this task sequence step to install the Configuration Manager client software. Configuration Manager installs and registers the Configuration Manager client GUID. You can assign the necessary installation parameters in the **Installation properties** window.|  
|Install Updates|Use this task sequence step to specify how software updates are installed on the destination computer. The destination computer isn't evaluated for applicable software updates until this task sequence step runs. At that point, the destination computer is evaluated for software updates similar to any other Configuration Manager-managed client.<br /><br /> This step uses the read-only **_SMSTSMediaType** task sequence variable. This task sequence step runs only if the value of the variable doesn't equal **FullMedia**.|  
|Restore User Files and Settings - **(New task sequence subgroup)**|Create another task sequence subgroup. This subgroup contains the steps needed to restore the user files and settings.|  
|Request User State Storage|Use this task sequence step to request access to a state migration point where the user state data is stored.|  
|Restore User Files and Settings|Use this task sequence step to run the User State Migration Tool (USMT) to restore user state and settings to a destination computer.|  
|Release User State Storage|Use this task sequence step to notify the state migration point that the user state data is no longer needed.|  
