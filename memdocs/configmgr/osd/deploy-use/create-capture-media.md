---
title: Create capture media
titleSuffix: Configuration Manager
description: Use capture media in Configuration Manager to capture an OS image from a reference computer.
ms.date: 05/02/2019
ms.service: configuration-manager
ms.subservice: osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create capture media

*Applies to: Configuration Manager (current branch)*

Capture media in Configuration Manager allows you to capture an OS image from a reference computer. Capture media contains the boot image that starts the reference computer and the task sequence that captures the OS image. Use capture media for the scenario to [Create a task sequence to capture an OS](create-a-task-sequence-to-capture-an-operating-system.md).  


## Prerequisites

Before you create capture media by using the Create Task Sequence Media Wizard, be sure that all of these conditions are met.

### Boot image

Consider the following points about the boot image that you use in the task sequence to deploy the OS:

- The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.
- Make sure that the boot image contains the network and storage drivers that are required to provision the destination computer.

### Distribute all content associated with the task sequence

Distribute all content that the task sequence requires to at least one distribution point. This content includes the boot image, OS image, and other associated files. The wizard gathers the content from the distribution point when it creates the capture media.

Your user account needs at least **Read** access rights to the content library on that distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### Prepare the removable USB drive

If you're using a removable USB drive, connect it to the computer where you run the Create Task Sequence Media wizard. The USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media.

### Create an output folder

Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, create a folder for the output files it creates. Media that it creates for a CD or DVD set is written as an .ISO file directly in the folder.


## Process

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence Media**. This action starts the Create Task Sequence Media Wizard.  

3. On the **Select Media Type** page, select **Capture media**.  

4. On the **Media Type** page, specify whether the media is a **Removable USB drive** or a **CD/DVD set**. Then configure the following options:  

    > [!IMPORTANT]  
    > Media uses a FAT32 file system. You can't create media on a USB drive whose content contains a file over 4 GB in size.  

    - If you select **Removable USB drive**, select the drive where you want to store the content.  

        - **Format removable USB drive (FAT32) and make bootable**: By default, let Configuration Manager prepare the USB drive. Many newer UEFI devices require a bootable FAT32 partition. However, this format also limits the size of files and overall capacity of the drive. If you've already formatted and configured the removable drive, disable this option.

    - If you select **CD/DVD set**, specify the capacity of the media (**Media size**) and the name and path of the output file (**Media file**). The wizard writes the output files to this location. For example: `\\servername\folder\outputfile.iso`  

        If the capacity of the media is too small to store the entire content, it creates multiple files. Then you need to store the content on multiple CDs or DVDs. When it requires multiple media files, Configuration Manager adds a sequence number to the name of each output file that it creates.  

        > [!IMPORTANT]  
        > If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.  

    - **Staging folder**<!--1359388-->: The media creation process can require a lot of temporary drive space. By default this location is similar to the following path: `%UserProfile%\AppData\Local\Temp`. Starting in version 1902, to give you greater flexibility with where to store these temporary files, change this value to another drive and path.  

    - **Media label**<!--1359388-->: Starting in version 1902, add a label to task sequence media. This label helps you better identify the media after you create it. The default value is `Configuration Manager`. This text field appears in the following locations:  

        - If you mount an ISO file, Windows displays this label as the name of the mounted drive  

        - If you format a USB drive, it uses the first 11 characters of the label as its name  

        - Configuration Manager writes a text file called `MediaLabel.txt` to the root of the media. By default, the file includes a single line of text: `label=Configuration Manager`. If you customize the label for media, this line uses your custom label instead of the default value.  

    - **Include autorun.inf file on media**<!-- 4090666 -->: Starting in version 1906, Configuration Manager doesn't add an autorun.inf file by default. This file is commonly blocked by antimalware products. For more information on the AutoRun feature of Windows, see [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay). If still necessary for your scenario, select this option to include the file.  

5. On the **Boot image** page, specify the following options:  

    > [!IMPORTANT]  
    > The architecture of the boot image that you distribute must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.  

    - **Boot image**: Select the boot image to start the destination computer.  

    - **Distribution point**: Select the distribution point that has the boot image. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        > Your user account needs at least **Read** permissions to the content library on the distribution point.  

6. Complete the wizard.  


## Next steps

[Create a task sequence to capture an OS](create-a-task-sequence-to-capture-an-operating-system.md)