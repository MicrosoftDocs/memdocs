---
title: Create stand-alone media
titleSuffix: Configuration Manager
description: Use stand-alone media to deploy the OS on a computer without a network connection.
ms.date: 03/10/2022
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create stand-alone media

*Applies to: Configuration Manager (current branch)*

Stand-alone media in Configuration Manager contains everything required to deploy the OS on a computer without a network connection.

Use stand-alone media with the following OS deployment scenarios:  

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md)  


## Usage

Stand-alone media includes the task sequence that automates the steps to install the OS, and all other required content. This content includes the boot image, OS image, and device drivers. Because the stand-alone media stores everything to deploy the OS, it requires more disk space than required for other types of media.

When you create stand-alone media on a CAS, the client retrieves its assigned site code from Active Directory. Stand-alone media created at child sites automatically assigns to the client the site code for that site.  


## Prerequisites

Before you create stand-alone media by using the Create Task Sequence Media Wizard, be sure that all of these conditions are met.

### Create a task sequence to deploy an OS

As part of the stand-alone media, specify the task sequence to deploy an OS. For more information, see [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md).

#### Unsupported actions for stand-alone media

The following actions aren't supported for stand-alone media:

- The [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) step in the task sequence. Stand-alone media doesn't support automatic application of device drivers from the driver catalog. Use the [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) step to make a specified set of drivers available to Windows Setup.  

- The [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) step in the task sequence. The management point information isn't available on stand-alone media, so the step fails trying to enumerate content locations.  

- Installing software updates.  

- Installing software before deploying the OS.  

- Custom task sequences for non-OS deployments.  

- Associating users with the destination computer to support user device affinity.  

- Dynamic package installs via the [Install Packages](../understand/task-sequence-steps.md#BKMK_InstallPackage) step.  

- Dynamic application installs via the [Install Application](../understand/task-sequence-steps.md#BKMK_InstallApplication) step.

- The **Use pre-production client package when available** setting in the **Setup Windows and ConfigMgr** task sequence step. For more information about this setting, see [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### Known issue with Install Package step and media created at the central administration site

An error might occur if your task sequence includes the [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) step and you create the stand-alone media at a central administration site (CAS). The CAS doesn't have the necessary client configuration policies. These policies are required to enable the software distribution agent when the task sequence runs. The following error might appear in the **CreateTsMedia.log** file: `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`

For stand-alone media that includes an **Install Package** step, create the stand-alone media at a primary site that has the software distribution agent enabled.

Alternatively, use a custom [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) step. Add it after the [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step and before the first **Install Package** step. The **Run PowerShell Script** step runs the following commands to enable the software distribution agent before the first Install Package step:

```powershell
$namespace = "root\ccm\policy\machine\requestedconfig"
$class = "CCM_SoftwareDistributionClientConfig"
$classArgs = @{
    ComponentName = 'Enable SWDist'
    Enabled = 'true'
    LockSettings='TRUE'
    PolicySource='local'
    PolicyVersion='1.0'
    SiteSettingsKey='1'
}
Set-WmiInstance -Namespace $namespace -Class $class -Arguments $classArgs -PutType CreateOnly
```

### Distribute all content associated with the task sequence

Distribute all content that the task sequence requires to at least one distribution point. This content includes the boot image, OS image, and other associated files. The wizard gathers the content from the distribution point when it creates the media.

Your user account needs at least **Read** access rights to the content library on that distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### Prepare the removable USB drive

If you're using a removable USB drive, connect it to the computer where you run the Create Task Sequence Media wizard. The USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media.

Stand-alone media uses a FAT32 file system. You can't create stand-alone media on a removable USB drive whose content contains a file over 4 GB in size.

### Create an output folder

Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, create a folder for the output files it creates. Media that it creates for a CD or DVD set is written as an .ISO file directly in the folder.


## Process

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence Media**. This action starts the Create Task Sequence Media Wizard.  

3. On the **Select Media Type** page, specify the following options:  

    - Select **Stand-alone media**.  

    - Optionally, if you want to only allow the OS to be deployed without requiring user input, select **Allow unattended operating system deployment**.  

        > [!IMPORTANT]  
        > When you select this option, the user isn't prompted for network configuration information or for optional task sequences. If you configure the media for password protection, the user is still prompted for a password.  

4. On the **Media Type** page, specify whether the media is a **Removable USB drive** or a **CD/DVD set**. Then configure the following options:  

    > [!IMPORTANT]  
    > Media uses a FAT32 file system. You can't create media on a USB drive whose content contains a file over 4 GB in size.  

    - If you select **Removable USB drive**, select the drive where you want to store the content.  

        - **Format removable USB drive (FAT32) and make bootable**: By default, let Configuration Manager prepare the USB drive. Many newer UEFI devices require a bootable FAT32 partition. However, this format also limits the size of files and overall capacity of the drive. If you've already formatted and configured the removable drive, disable this option.

    - If you select **CD/DVD set**, specify the capacity of the media (**Media size**) and the name and path of the output file (**Media file**). The wizard writes the output files to this location. For example: `\\servername\folder\outputfile.iso`  

        If the capacity of the media is too small to store the entire content, it creates multiple files. Then you need to store the content on multiple CDs or DVDs. When it requires multiple media files, Configuration Manager adds a sequence number to the name of each output file that it creates.  

        If you deploy an application along with the OS, and the application can't fit on a single media, Configuration Manager stores the application across multiple media. When the stand-alone media is run, Configuration Manager prompts the user for the next media where the application is stored.  

        > [!IMPORTANT]  
        > If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.  

    - **Staging folder**<!--1359388-->: The media creation process can require a lot of temporary drive space. By default this location is similar to the following path: `%UserProfile%\AppData\Local\Temp`. To give you greater flexibility with where to store these temporary files, change this value to another drive and path.  

    - **Media label**<!--1359388-->: Add a label to task sequence media. This label helps you better identify the media after you create it. The default value is `Configuration Manager`. This text field appears in the following locations:  

        - If you mount an ISO file, Windows displays this label as the name of the mounted drive  

        - If you format a USB drive, it uses the first 11 characters of the label as its name  

        - Configuration Manager writes a text file called `MediaLabel.txt` to the root of the media. By default, the file includes a single line of text: `label=Configuration Manager`. If you customize the label for media, this line uses your custom label instead of the default value.  

    - **Include autorun.inf file on media**<!-- 4090666 -->: Configuration Manager doesn't add an autorun.inf file by default. This file is commonly blocked by antimalware products. For more information on the AutoRun feature of Windows, see [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay). If still necessary for your scenario, select this option to include the file.  

5. On the **Security** page, specify the following options:

    - **Protect media with a password**: Enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the media.  

        > [!IMPORTANT]  
        > As a security best practice, always assign a password to help protect the media.  
        >
        > On stand-alone media, it only encrypts the task sequence steps and their variables. It doesn't encrypt the remaining content of the media. Don't include any sensitive information in task sequence scripts. Store and implement all sensitive information by using task sequence variables.  

    - **Select date range for this stand-alone media to be valid**: Set optional start and expiration dates on the media. This setting is disabled by default. The dates are compared to the system time on the computer before the stand-alone media runs. When the system time is earlier than the start time or later than the expiration time, the stand-alone media doesn't start. These options are also available by using the [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia) PowerShell cmdlet.  

6. On the **Stand-Alone CD/DVD** page, select the task sequence that deploys the OS. You can only select those task sequences that are associated with a boot image. Verify the list of content referenced by the task sequence.  

    - **Detect associated application dependencies and add them to this media**: Also add content to the media for application dependencies.  

        > [!TIP]  
        > If you don't see expected application dependencies, deselect and then reselect this option to refresh the list.  

7. On the **Select Application** page, specify additional application content to include as part of the media file.  

8. On the **Select Package** page, specify additional package content to include as part of the media file.  

9. On the **Select Driver Package** page, specify additional driver package content to include as part of the media file.  

10. On the **Distribution Points** page, specify the distribution points that contain the required content.  

    Configuration Manager only displays distribution points that have the content. Distribute all of the content associated with the task sequence to at least one distribution point before you continue. After you distribute the content, refresh the distribution point list. Remove any distribution points that you already selected on this page, go to the previous page, and then back to the **Distribution Points** page. Alternatively, restart the wizard. For more information, see [Distribute referenced content](distribute-task-sequence-referenced-content.md) and [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. On the **Customization** page, specify the following options:  

    - Add any variables that the task sequence uses.  

    - **Enable prestart command**: Specify any prestart commands that you want to run before the task sequence runs. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs. For more information, see [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > During media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the **CreateTSMedia.log** file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

        If the prestart command requires any content, select the option to **Include files for the prestart command**.  

12. Complete the wizard.  

The stand-alone media files (.ISO) are created in the destination folder. If you selected **CD/DVD set**, copy the output files to a set of CDs or DVDs.


## Next steps

[Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
