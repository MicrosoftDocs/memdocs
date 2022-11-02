---
title: Create a task sequence to capture an OS
titleSuffix: Configuration Manager
description: A build-and-capture task sequence builds a reference computer that can include specific drivers and software updates along with the OS.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create a task sequence to capture an OS

*Applies to: Configuration Manager (current branch)*

When you use a task sequence to deploy an OS to a computer in Configuration Manager, the computer installs the OS image that you specify in the task sequence. You can customize the OS image so it includes specific applications and software updates. First use a build and capture task sequence to build a reference computer. Then capture the OS image from that reference computer. If you already have a reference computer available to capture, create a custom task sequence to capture the OS.

> [!NOTE]  
> To avoid potential hardware driver issues when deploying custom reference images to different model devices, it is recommended to create custom reference images using virtual machines (VMs). This minimizes the amount of potentially conflicting drivers that are included as part of the custom reference image. Additionally it is recommended not to add any drivers to the custom reference image via either the **Auto Apply Drivers** task or the **Apply Driver Package** task.

## <a name="BKMK_BuildCaptureTS"></a> About the build and capture task sequence

The build and capture task sequence:

- Partitions and formats the reference computer
- Installs the OS
- Installs the Configuration Manager client
- Installs applications
- Applies software updates
- Captures the OS from the reference computer

The packages associated with the task sequence, such as applications, must be available on distribution points before you deploy the build and capture task sequence.

## <a name="BKMK_CreatePackages"></a> Requirements

Before you create a task sequence to install an OS, make sure the following components are in place:  

### Required

- [Boot image](../get-started/manage-boot-images.md)

- [OS image](../get-started/manage-operating-system-images.md)

### Required (if used)

- [Driver packages](../get-started/manage-drivers.md) that contain the necessary Windows drivers to support hardware on the reference computer. For more information about the task sequence steps to manage drivers, see [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Software updates](../../sum/get-started/synchronize-software-updates.md)

- [Applications](../../apps/deploy-use/create-applications.md)

## <a name="BKMK_CreateBuildCaptureTS"></a> Create a build and capture task sequence

Use the following procedure to use a task sequence to build a reference computer and capture the OS.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Task Sequences** node.  

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence** to start the Create Task Sequence Wizard.  

1. On the **Create a New Task Sequence** page, select **Build and capture a reference operating system image**.  

1. On the **Task Sequence Information** page, specify the following settings:  

    - **Task sequence name**: Specify a name that identifies the task sequence.  

    - **Description**: Specify an optional description for the task sequence. For example, describe the OS that the task sequence creates.

    - **Boot image**: Specify the boot image to use with this task sequence.  

        > [!IMPORTANT]  
        > The architecture of the boot image must be compatible with the hardware architecture of the destination computer.  

1. On the **Install Windows** page, specify the following settings:  

    - **Image package**: Specify the OS image package, which contains the required files to install the OS.  

    - **Image index**: Specify the index of the OS to install in the image. If the OS image contains multiple versions, select the version that you want to install.  

    - **Product key**: If necessary, specify the product key for the Windows OS to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, separate each group of five characters with a dash (`-`). For example: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Server licensing mode**: If necessary, specify that the server license is **Per seat**, **Per server**, or that no license is specified. If the server license is **Per server**, also specify the maximum number of server connections.  

    - Specify how to configure the administrator account for the deployed OS:  

        - **Randomly generate the local administrator password and disable the account on all supported platforms**: Create a random password for the local administrator account. Disable the account when the Windows is set up.

        - **Enable the account and specify the local administrator password**: Use the same password for the local administrator account on all computers where you deploy this OS.

1. On the **Configure Network** page, specify the following settings:

    - **Join a workgroup**: Specify whether to add the destination computer to a workgroup when the OS is deployed.  

    - **Join a domain**: Specify whether to add the destination computer to a domain when the OS is deployed. In **Domain**, specify the name of the domain.  

        > [!IMPORTANT]  
        > You can browse to locate domains in the local forest. Specify the domain name for a remote forest.

        You can also specify an organizational unit (OU). This setting is optional, and specifies the LDAP X.500 distinguished name of the OU in which to create the computer account, if it doesn't already exist.  

    - **Account**: Specify the user name and password for the account that has permissions to join the specified domain. For example: `domain\user` or `%variable%`.  

        > [!IMPORTANT]  
        > If you plan to migrate either the domain settings or the workgroup settings during the deployment, make sure you enter the appropriate domain credentials here.  

1. On the **Install Configuration Manager** page, specify the Configuration Manager client package. This package contains the source files to install the Configuration Manager client. Also specify any additional properties needed to install the client.  

    For more information, see [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md).

1. On the **Include Updates** page, specify whether to install required software updates, all software updates, or no software updates. If you specify to install software updates, Configuration Manager installs only those software updates that are targeted to the collections that the destination computer is a member of.  

1. On the **Install Applications** page, specify the applications to install on the destination computer. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

    > [!NOTE]
    > The **System Preparation** page appears next in the wizard, but it's no longer used. Select **Next** to continue.

1. On the **Images Properties** page, specify the following settings for the OS image:

    - **Created by**: Specify the name of the user to note as the creator of the OS image.  

    - **Version**: Specify your version number that's associated with the OS image. This attribute doesn't need to be the OS version, as the site stores that value separately.

    - **Description**: Specify your description of the OS image.  

1. On the **Capture Image** page, specify the following settings:

    - **Path**: Specify a shared network folder where Configuration Manager should store the output image file (.wim). This file contains the OS image that's based on the settings you specify in this wizard. If you specify a folder that contains an existing .WIM file, it's overwritten.  

    - **Account**: Specify the Windows account that has permissions to the network share where the image is stored.  

1. Complete the wizard.  

To add additional steps to the task sequence, select it, and choose **Edit**. For more information about how to edit a task sequence, see [Use the task sequence editor](../understand/task-sequence-editor.md).  

Deploy the task sequence to a reference computer in one of the following ways:  

- If the reference computer is already a Configuration Manager client, deploy the build and capture task sequence to a collection that contains the reference computer. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

- If the reference computer isn't a Configuration Manager client, or if you want to manually run the task sequence on the reference computer, use the **Create Task Sequence Media Wizard** to create bootable media. For more information, see [Create bootable media](create-bootable-media.md).  

After you capture the image, you can deploy it to other computers. For more information about how to deploy the captured OS image, see [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="BKMK_CaptureExistingRefComputer"></a> Capture from an existing reference computer

When you already have a reference computer ready to capture, create a task sequence that only captures the OS from the reference computer. Use the **Capture Operating System Image** task sequence step to capture one or more images from a reference computer and store them in an image file (.wim) on the specified network share. Start the reference computer in Windows PE with a boot image. The task sequence captures each hard drive on the reference computer as a separate image within the .wim file. If the referenced computer has multiple drives, the resulting .wim file contains a separate image for each volume. It only captures volumes that are formatted as NTFS or FAT32. It skips volumes with other formats or USB volumes.  

Use the following procedure to capture an OS image from an existing reference computer:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Task Sequences** node.  

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence**. This action starts the Create Task Sequence Wizard.  

1. On the **Create a New Task Sequence** page, select **Create a new custom task sequence**.  

1. On the **Task Sequence Information** page, specify a name for the task sequence. Optionally add a description for the task sequence.  

1. Specify a boot image for the task sequence. Configuration Manager uses this boot image to start the reference computer with Windows PE. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

1. Complete the wizard.  

1. In the **Task Sequences** node, select the new task sequence. Then on the **Home** tab of the ribbon, in the **Task Sequence** group, select **Edit**. This action opens the task sequence editor.  

1. If the Configuration Manager client is installed on the reference computer:

    Go to the **Add** menu, select **Images**, and then choose [Prepare ConfigMgr Client for Capture](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). This step generalizes the Configuration Manager client on the reference computer.

    > [!Note]  
    > The task sequence doesn't support uninstalling the Configuration Manager client.

1. Go to the **Add** menu, select **Images**, and choose [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). This step runs Sysprep, and then restarts the computer to the Windows PE boot image specified for the task sequence. For this action to complete successfully, don't join the reference computer to a domain.

1. Go to the **Add** menu, select **Images**, and choose [Capture Operating System Image](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). This step only runs from Windows PE to capture the hard drives on the reference computer. Configure the following settings:

    - **Name** and **Description**: Optionally, you can change the name of the task sequence step and provide a description.  

    - **Destination**: Specify a shared network folder where the output .WIM file is stored. This file contains the OS image based on the settings that you specify by using this wizard. If you specify a folder that contains an existing .WIM file, it's overwritten.  

    - **Description**, **Version**, and **Created by**: Optionally, provide details about the image to capture.  

    - **Capture operating system image account**: Specify the Windows account that has permissions to the network share you specified. Select **Set** to specify the name of that Windows account.  

Select **OK** to save your changes and close the task sequence editor.  

Deploy the task sequence to a reference computer in one of the following ways:  

- If the reference computer is already a Configuration Manager client, deploy the capture task sequence to a collection that contains the reference computer. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

- If the reference computer isn't a Configuration Manager client, or if you want to manually run the task sequence on the reference computer, use the **Create Task Sequence Media Wizard** to create capture media. For more information, see [Create capture media](create-capture-media.md).  

After you capture the image, you can deploy it to other computers. For more information about how to deploy the captured OS image, see [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="BKMK_BuildandCaptureTSExample"></a> Example task sequence

Use the following table as a guide as you create a task sequence that builds and captures an OS image. The table helps you decide the general sequence for your task sequence steps, and how to organize and structure those steps into logical groups. The task sequence that you create may vary from this sample. It can contain more or less steps and groups.

> [!NOTE]  
> Always use the Create Task Sequence Wizard to create this type of task sequence.
>
> The wizard adds steps to the task sequence with slightly different names that what you'd see if you manually add the same steps.

### Group: Build the Reference Machine

This group contains the actions necessary to build a reference computer.

|Task sequence step|Description|  
|-------------------------------|---------------|  
|**Restart in Windows PE**|Restart the destination computer to the boot image assigned to the task sequence. This step displays a message to the user that the computer will be restarted so that the installation can continue.<br /><br />This step uses the read-only `_SMSTSInWinPE` task sequence variable. If the associated value equals `false`, then the task sequence step continues.|
|**Partition Disk 0 - BIOS**|Partition and format the hard drive on the destination computer in BIOS mode. The default disk number is `0`.<br /><br />This step uses several read-only task sequence variables. For example, it only runs if the Configuration Manager client cache doesn't exist, and doesn't run if the computer is configured for UEFI.|
|**Partition Disk 0 - UEFI**|Partition and format the hard drive on the destination computer in UEFI mode. The default disk number is `0`.<br /><br />This step uses several read-only task sequence variables. For example, it only runs if the Configuration Manager client cache doesn't exist, and only runs if the computer is configured for UEFI.|
|**Apply Operating System**|Install the specified OS image on the destination computer. This step first deletes all files on the volume, other than Configuration Manager-specific control files. It then applies all volume images contained in the WIM file to the corresponding sequential disk volume on the target computer.|
|**Apply Windows Settings**|Configure the Windows settings for the destination computer.|
|**Apply Network Settings**|Specify the network or workgroup configuration information for the destination computer.|
|**Apply Device Drivers**|Match and install drivers as part of this OS deployment. For more information, see [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />This step uses the read-only `_SMSTSMediaType` task sequence variable. If the associated value doesn't equal `FullMedia`, this step doesn't run.|
|**Setup Windows and Configuration Manager**|Install the Configuration Manager client software. Configuration Manager installs and registers the Configuration Manager client GUID. Include any necessary **Installation properties**.|
|**Install Updates**|Specify how software updates are installed on the destination computer. The destination computer isn't evaluated for applicable software updates until this step runs. At that point, the evaluation is similar to any other Configuration Manager-managed client. For more information, see [Install Software Updates](../understand/install-software-updates.md).<br /><br />This step uses the read-only `_SMSTSMediaType` task sequence variable. If the associated value doesn't equal `FullMedia`, this step doesn't run.|
|**Install Applications**|Specifies any applications to install on the reference computer.|

### Group: Capture the Reference Machine

This group contains the necessary steps to prepare and capture a reference computer.

|Task sequence step|Description|  
|-------------------------------|---------------|  
|**Prepare Configuration Manager Client**|Generalize the Configuration Manager client on the reference computer.|
|**Prepare OS**|Runs Sysprep to generalize Windows. It then restarts the computer into the Windows PE boot image specified for the task sequence.|
|**Capture the Reference Machine**|Captures the image to the specified network share and .WIM file.|

> [!IMPORTANT]
> After you capture an image from a reference computer, don't capture another OS image from the reference computer. Registry entries are created during the initial configuration. Create a new reference computer each time that you capture the OS image. If you plan to use the same reference computer to create future OS images, first uninstall and reinstall the Configuration Manager client.

## Next steps

[Methods to deploy enterprise operating systems](methods-to-deploy-enterprise-operating-systems.md)
