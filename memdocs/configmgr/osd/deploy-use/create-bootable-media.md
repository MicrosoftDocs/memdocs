---
title: Create bootable media
titleSuffix: Configuration Manager
description: Use bootable media in Configuration Manager to install a new version of Windows or replace a computer.
ms.date: 08/25/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create bootable media

*Applies to: Configuration Manager (current branch)*

Bootable media in Configuration Manager contains the boot image, optional prestart commands and associated files, and Configuration Manager files. Use bootable media for the following OS deployment scenarios:

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)

## Usage

The following process occurs when you boot to bootable media:

1. The destination computer starts

1. It connects to the network

1. It retrieves the following content from the site:

    - The specified task sequence

    - OS image

    - Any other required content

Because the task sequence isn't on the media, you can change the task sequence or content without having to recreate the media.

The packages on bootable media aren't encrypted. To make sure that the package contents are secured from unauthorized users, take appropriate security measures. For example, add a password to the media.

Starting in version 2006, bootable media can download cloud-based content. The device still needs an intranet connection to the management point. It can get content from a content-enabled cloud management gateway (CMG).<!--6209223--> For more information, see [Bootable media support for cloud-based content](deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content).

## Prerequisites

Before you create bootable media by using the Create Task Sequence Media Wizard, be sure that all of these conditions are met.

### Boot image

Consider the following points about the boot image that you use in the task sequence to deploy the OS:

- The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.
- Make sure that the boot image contains the network and storage drivers that are required to provision the destination computer.

### Create a task sequence to deploy an OS

As part of the bootable media, specify the task sequence to deploy the OS. For more information, see [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md).

### Distribute all content associated with the task sequence

Distribute all content that the task sequence requires to at least one distribution point. This content includes the boot image and other associated prestart files. The wizard gathers the content from the distribution point when it creates the bootable media.

Your user account needs at least **Read** access rights to the content library on that distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### Prepare the removable USB drive

If you're using a removable USB drive, connect it to the computer where you run the Create Task Sequence Media wizard. The USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media.

### Create an output folder

Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, create a folder for the output files it creates. Media that it creates for a CD or DVD set is written as an .ISO file directly in the folder.

## Process

> [!NOTE]
> For PKI environments, since you specify the root certificate authority (CA) at the primary site, make sure to create the bootable media at the primary site. The central administration site (CAS) doesn't have the root CA information to properly create the bootable media. For more technical information on this issue, see [Sending with winhttp failed 80072f8f error in Smsts.log during OS deployment by using bootable or prestaged media](/troubleshoot/mem/configmgr/sending-with-winhttp-failed-80072f8f-error).

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence Media**. This action starts the Create Task Sequence Media Wizard.

1. On the **Select Media Type** page, specify the following options:

    - Select **Bootable media**.

    - Optionally, if you want to only allow the OS to be deployed without requiring user input, select **Allow unattended operating system deployment**.

        > [!IMPORTANT]
        > When you select this option, the user isn't prompted for network configuration information or for optional task sequences. If you configure the media for password protection, the user is still prompted for a password.

1. On the **Media Management** page, specify one of the following options:

    - **Dynamic media**: Allow a management point to redirect the media to another management point, based on the client location in the site boundaries.

    - **Site-based media**: The media only contacts the specified management point.

1. On the **Media Type** page, specify whether the media is a **Removable USB drive** or a **CD/DVD set**. Then configure the following options:

    > [!IMPORTANT]
    > Media uses a FAT32 file system. You can't create media on a USB drive whose content contains a file over 4 GB in size.

    - If you select **Removable USB drive**, select the drive where you want to store the content.

        - **Format removable USB drive (FAT32) and make bootable**: By default, let Configuration Manager prepare the USB drive. Many newer UEFI devices require a bootable FAT32 partition. However, this format also limits the size of files and overall capacity of the drive. If you've already formatted and configured the removable drive, disable this option.

    - If you select **CD/DVD set**, specify the capacity of the media (**Media size**) and the name and path of the output file (**Media file**). The wizard writes the output files to this location. For example: `\\servername\folder\outputfile.iso`

        If the capacity of the media is too small to store the entire content, it creates multiple files. Then you need to store the content on multiple CDs or DVDs. When it requires multiple media files, Configuration Manager adds a sequence number to the name of each output file that it creates.

        > [!IMPORTANT]
        > If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.

    - **Staging folder**<!--1359388-->: The media creation process can require much temporary drive space. By default this location is similar to the following path: `%UserProfile%\AppData\Local\Temp`. To give you greater flexibility with where to store these temporary files, you can change this value to another drive and path.

    - **Media label**<!--1359388-->: Add a label to task sequence media. This label helps you better identify the media after you create it. The default value is `Configuration Manager`. This text field appears in the following locations:

        - If you mount an ISO file, Windows displays this label as the name of the mounted drive.

        - If you format a USB drive, it uses the first 11 characters of the label as its name.

        - Configuration Manager writes a text file called `MediaLabel.txt` to the root of the media. By default, the file includes a single line of text: `label=Configuration Manager`. If you customize the label for media, this line uses your custom label instead of the default value.

    - **Include autorun.inf file on media**<!-- 4090666 -->: Configuration Manager doesn't add an autorun.inf file by default. This file is commonly blocked by antimalware products. For more information on the AutoRun feature of Windows, see [Creating an AutoRun-enabled CD-ROM Application](/windows/desktop/shell/autoplay). If still necessary for your scenario, select this option to include the file.

1. On the **Security** page, specify the following options:

    - **Enable unknown computer support**: Allow the media to deploy an OS to a computer that's not managed by Configuration Manager. There's no record of these computers in the Configuration Manager database. For more information, see [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md).

    - **Protect media with a password**: Enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the bootable media.

        > [!IMPORTANT]
        > As a security best practice, always assign a password to help protect the bootable media.

    - For HTTP communications, select **Create self-signed media certificate**. Then specify the start and expiration date for the certificate.

        > [!NOTE]
        > If you select this option, you can't select any HTTPS management point on the **Boot image** page of this wizard.

    - For HTTPS communications, select **Import PKI certificate**. Then specify the certificate to import and its password.

        For more information about this client certificate that boot images use, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md).

    - **User device affinity**: To support user-centric management in Configuration Manager, specify how you want the media to associate users with the destination computer. For more information about how OS deployment supports user device affinity, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).

        - **Allow user device affinity with auto-approval**: The media automatically associates users with the destination computer. This functionality is based on the actions of the task sequence that deploys the OS. In this scenario, the task sequence creates a relationship between the specified users and destination computer when it deploys the OS to the destination computer.

        - **Allow user device affinity pending administrator approval**: The media associates users with the destination computer after approval is granted. This functionality is based on the scope of the task sequence that deploys the OS. In this scenario, the task sequence creates a relationship between the specified users and the destination computer. It then waits for approval from an administrative user before it deploys the OS.

        - **Do not allow user device affinity**: The media doesn't associate users with the destination computer. In this scenario, the task sequence doesn't associate users with the destination computer when it deploys the OS.

1. On the **Boot image** page, specify the following options:

    > [!IMPORTANT]
    > The architecture of the boot image that you distribute must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can only boot and run an x86 boot image.

    - **Boot image**: Select the boot image to start the destination computer.

    - **Distribution point**: Select the distribution point that has the boot image. The wizard retrieves the boot image from the distribution point and writes it to the media.

        > [!NOTE]
        > Your user account needs at least **Read** permissions to the content library on the distribution point.

    - **Management point**: Only for *site-based media*, select a management point from a primary site.

    - **Associated management points**: Only for *dynamic media*, select the primary site management points to use, and a priority order for the initial communication.

        > [!NOTE]
        > When you specify a PKI certificate on the **Security** page of this wizard, this page only displays HTTPS-enabled management points.

1. On the **Customization** page, specify the following options:

    - Add any variables that the task sequence uses.

    - **Enable prestart command**: Specify any prestart commands that you want to run before the task sequence runs. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs. For more information, see [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).

        > [!TIP]
        > During media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the **CreateTSMedia.log** file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.

        If the prestart command requires any content, select the option to **Include files for the prestart command**.

1. Complete the wizard.

## Alternate method

You can create bootable media on a removable USB drive when the drive isn't connected to the computer running the Configuration Manager console.

1. [Create the task sequence boot media](#process). On the **Media type** page, select **CD/DVD set**. The wizard writes the output files to the location that you specify. For example: `\\servername\folder\outputfile.iso`.  

1. Prepare the removable USB drive. The drive must be formatted, empty, and bootable.

1. Mount the ISO from the share location and transfer the files from the ISO to the USB drive.

## Next steps

[Use bootable media to deploy Windows over the network](use-bootable-media-to-deploy-windows-over-the-network.md)
