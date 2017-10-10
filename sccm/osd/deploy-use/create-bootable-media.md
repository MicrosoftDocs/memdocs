---
title: "Create bootable media "
description: "Bootable media in Configuration Manager make it easy to install a new version of Windows or replace a computer and transfer settings."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Create bootable media with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Bootable media in Configuration Manager contains the boot image, optional prestart commands and associated files, and Configuration Manager files. Use prestaged media for the following operating system deployment scenarios:  

-   [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Create bootable media  
 When you boot to the bootable media, the destination computer starts, connects to the network and retrieves the specified task sequence, operating system image, and any other required content from the network. Because the task sequence is not on the media, you can change the task sequence or content without having to recreate the media. The packages on bootable media are not encrypted. You must take the appropriate security measures, such as adding a password to the media, to ensure that the package contents are secured from unauthorized users.  

 Before you create bootable media by using the Create Task Sequence Media Wizard, be sure that all the following conditions are met:  

|Task|Description|  
|----------|-----------------|  
|Boot image|Consider the following about the boot image that you will use in the task sequence to deploy the operating system:<br /><br /> -   The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.<br />-   Ensure that the boot image contains the network and mass storage drivers that are required to provision the destination computer.|  
|Create a task sequence to deploy an operating system|As part of the bootable media, you must specify the task sequence to deploy the operating system. For the steps to create a new task sequence, see [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Distribute all content associated with the task sequence|You must distribute to at least one distribution point all content that is required by the task sequence. This includes the boot image and other associated prestart files. The wizard gathers the information from the distribution point when it creates the bootable media. You must have **Read** access rights to the content library on that distribution point.  For details, see [About the content library](../../core/plan-design/hierarchy/the-content-library.md).|  
|Prepare the removable USB drive|For a removable USB drive:<br /><br /> If you are going to use a removable USB drive, the USB  drive must be connected to the computer where the wizard is run and the USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media. Stand-alone media uses a FAT32 file system. You cannot create stand-alone media on a USB flash drive whose content contains a file over 4 GB in size.|  
|Create an output folder|For a CD/DVD set:<br /><br /> Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, you must create a folder for the output files created by the wizard. Media that is created for a CD or DVD set is written as .iso files directly to the folder.|  

 Use the following procedure to create bootable media.  

### To create bootable media  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence Media** to start the Create Task Sequence Media Wizard.  

4.  On the **Select Media Type** page, specify the following options, and then click **Next**.  

    -   Select **Bootable media**.  

    -   Optionally, if you want to only allow the operating system to be deployed without requiring user input, select **Allow unattended operating system deployment**.  

        > [!IMPORTANT]  
        >  When you select this option, the user is not prompted for network configuration information or for optional task sequences. However, the user is still prompted for a password if the media is configured for password protection.  

5.  On the **Media Management** page, specify one of the following options, and then click **Next**.  

    -   Select **Dynamic media** if you want to allow a management point to redirect the media to another management point, based on the client location in the site boundaries.  

    -   Select **Site-based media** if you want the media to contact only the specified management point.  

6.  On the **Media Type** page, specify whether the media is a flash drive or a CD/DVD set, and then click configure the following:  

    > [!IMPORTANT]  
    >  Stand-alone media uses a FAT32 file system. You cannot create stand-alone media on a USB flash drive whose content contains a file over 4 GB in size.  

    -   If you select **USB flash drive**, specify the drive where you want to store the content.  

    -   If you select **CD/DVD set**, specify the capacity of the media and the name and path of the output files. The wizard writes the output files to this location. For example: **\\\servername\folder\outputfile.iso**  

         If the capacity of the media is too small to store the entire content, multiple files are created and you must store the content on multiple CDs or DVDs. When multiple media is required, Configuration Manager adds a sequence number to the name of each output file that it creates. In addition, if you deploy an application along with the operating system and the application cannot fit on a single media, Configuration Manager stores the application across multiple media. When the stand-alone media is run, Configuration Manager prompts the user for the next media where the application is stored.  

        > [!IMPORTANT]  
        >  If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.  

     Click **Next**.  

7.  On the **Security** page, specify the following options, and then click **Next**.  

    -   Select the **Enable unknown computer support** check box to allow the media to deploy an operating system to a computer that is not managed by Configuration Manager. There is no record of these computers in the Configuration Manager database.  

         Unknown computers include the following:  

        -   A computer where the Configuration Manager client is not installed  

        -   A computer that is not imported into Configuration Manager  

        -   A computer that is not discovered by Configuration Manager  

    -   Select the **Protect the media with a password** check box and enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the bootable media.  

        > [!IMPORTANT]  
        >  As a security best practice, always assign a password to help protect the bootable media.  

    -   For HTTP communications, select **Create self-signed media certificate**, and then specify the start and expiration date for the certificate.  

    -   For HTTPS communications, select **Import PKI certificate**, and then specify the certificate to import and its password.  

         For more information about this client certificate that is used for boot images, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **User Device Affinity**: To support user-centric management in Configuration Manager, specify how you want the media to associate users with the destination computer. For more information about how operating system deployment supports user device affinity, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

        -   Specify **Allow user device affinity with auto-approval** if you want the media to automatically associate users with the destination computer. This functionality is based on the actions of the task sequence that deploys the operating system. In this scenario, the task sequence creates a relationship between the specified users and destination computer when it deploys the operating system to the destination computer.  

        -   Specify **Allow user device affinity pending administrator approval** if you want the media to associate users with the destination computer after approval is granted. This functionality is based on the scope of the task sequence that deploys the operating system.  In this scenario, the task sequence creates a relationship between the specified users and the destination computer, but waits for approval from an administrative user before the operating system is deployed.  

        -   Specify **Do not allow user device affinity** if you do not want the media to associate users with the destination computer. In this scenario, the task sequence does not associate users with the destination computer when it deploys the operating system.  

8.  On the **Boot image** page, specify the following options, and then click **Next**.  

    > [!IMPORTANT]  
    >  The architecture of the boot image that is distributed must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.  

    -   In the **Boot image** box, specify the boot image to start the destination computer.  

    -   In the **Distribution point** box, specify the distribution point where the boot image resides. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        >  You must have **Read** access rights to the content library on the distribution point.  

    -   If you create site-based bootable media on the **Media Management** page of the wizard, specify a management point from a primary site in the **Management point** box.  

    -   If you create dynamic bootable media on the **Media Management** page of the wizard, specify the primary site management points to use, and a priority order for the initial communications in **Associated management points**.  

9. On the **Customization** page, specify the following options, and then click **Next**.  

    -   Specify the variables that the task sequence uses to deploy the operating system.  

    -   Specify any prestart commands that you want to run before the task sequence runs. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs to install the operating system. For more information, see [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  During task sequence media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the CreateTSMedia.log log file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

         Optionally, select the **Files for the prestart command** check box to include any required files for the prestart command.  

10. Complete the wizard.  

## Create bootable media on a USB drive from a network share
The information in this section helps you to create bootable media on a USB flash drive when the flash drive is not connected to the computer running the Configuration Manager console. To create the bootable media on the USB drive, you can create task sequence boot media, mount the ISO, and transfer the files from the ISO to the USB drive.

1. [Create the task sequence boot media](#to-create-task-boobable-media). On the **Media type** page, select **CD/DVD set**. The wizard writes the output files to the location that you specify. For example: **\\\servername\folder\outputfile.iso**.  
2. Prepare the removable USB drive. The drive must be formatted, empty, and bootable.
3. Mount the ISO from the share location and transfer the files from the ISO to the USB drive.

## Next steps  
[Use bootable media to deploy Windows over the network](use-bootable-media-to-deploy-windows-over-the-network.md)  
