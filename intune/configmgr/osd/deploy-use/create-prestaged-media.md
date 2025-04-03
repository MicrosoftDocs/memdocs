---
title: Create prestaged media
titleSuffix: Configuration Manager
description: Use prestaged media in Configuration Manager to simplify deployment of Windows in several scenarios.
ms.date: 12/14/2023
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

# Create prestaged media

*Applies to: Configuration Manager (current branch)*

Prestaged media in Configuration Manager is a Windows Image (WIM) file. It can be installed on a bare-metal computer by the manufacturer or at your staging center that's not connected to the production Configuration Manager environment. Prestaged media contains the boot image used to start the destination computer and the OS image that's applied to the destination computer. You can also specify applications, packages, and driver packages to include as part of the prestaged media. The task sequence that deploys the OS isn't included in the media. Prestaged media is applied to the hard drive of a new computer before the computer is sent to the end user.

Use prestaged media for the following OS deployment scenarios:  

- [Create an image for an OEM in factory or a local depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Deploy Windows to Go](deploy-windows-to-go.md)  


## Usage

When the computer starts for the first time after you've applied the prestaged media, the computer starts in Windows PE. It connects to a management point to locate the task sequence that completes the OS deployment process. When you deploy a task sequence that uses prestaged media, the client checks the local task sequence cache for valid content first. If the content can't be found or has been revised, the client downloads the content from a distribution point or peer.  


## Prerequisites

Before you create prestaged media by using the Create Task Sequence Media Wizard, be sure that all of the conditions are met.

### Boot image

Consider the following points about the boot image that you use in the task sequence to deploy the OS:

- The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.
- Make sure that the boot image contains the network and storage drivers that are required to provision the destination computer.

### Create a task sequence to deploy an OS

As part of the prestaged media, specify the task sequence to deploy the OS. For more information, see [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md).

### Distribute all content associated with the task sequence

Distribute all content that the task sequence requires to at least one distribution point. This content includes the boot image, OS image, and other associated files. The wizard gathers the content from the distribution point when it creates the prestaged media.

Your user account needs at least **Read** access rights to the content library on that distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### Hard drive on the destination computer

The hard drive of the destination computer must be formatted before the prestaged media is applied to it. If the hard drive isn't formatted when the media is applied, the task sequence that deploys the OS fails when it attempts to start the destination computer.

> [!NOTE]  
> The Create Task Sequence Media Wizard sets the following task sequence variable condition on the media: **_SMSTSMediaType = OEMMedia**. You can use this same condition in your task sequence.  


## Process

 > [!NOTE]  
 > For PKI environments, since the Root CA is specified at the Primary site, make sure the prestaged media is created at the Primary site. The CAS site does not have the Root CA information to properly create the prestaged media.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence Media**. This action starts the Create Task Sequence Media Wizard.  

3. On the **Select Media Type** page, specify the following options:  

    - Select **Prestaged media**.  

    - Optionally, if you want to only allow the OS to be deployed without requiring user input, select **Allow unattended operating system deployment**.  

        > [!IMPORTANT]  
        > When you select this option, the user isn't prompted for network configuration information or for optional task sequences. If you configure the media for password protection, the user is still prompted for a password.  

4. On the **Media Management** page, specify one of the following options:  

    - **Dynamic media**: Allow a management point to redirect the media to another management point, based on the client location in the site boundaries.  

    - **Site-based media**: The media only contacts the specified management point.  

5. On the **Media Properties** page, specify the following information:  

    - **Created by**: Specify who created the media.  

    - **Version**: Specify the version number of the media.  

    - **Comment**: Specify a unique description of what the media is used for.  

    - **Media file**: Specify the name and path of the output files. The wizard writes the output files to this location. For example: `\\servername\folder\outputfile.wim`  

    - **Staging folder**<!--1359388-->: The media creation process can require a lot of temporary drive space. By default this location is similar to the following path: `%UserProfile%\AppData\Local\Temp`. To give you greater flexibility with where to store these temporary files, change this value to another drive and path.

6. On the **Security** page, specify the following options:  

    - **Enable unknown computer support**: Allow the media to deploy an OS to a computer that's not managed by Configuration Manager. There's no record of these computers in the Configuration Manager database. For more information, see [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Protect media with a password**: Enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the prestaged media.  

        > [!IMPORTANT]  
        > As a security best practice, always assign a password to help protect the prestaged media. Assigning a password to the media not only prevents someone without the password from running a task sequence when using the media, but it also properly encrypts the task sequence environment on the media. The task sequence environment includes the task sequence steps and their variables.
        >
        > Using a password doesn't encrypt the remaining content of the prestaged media such as packages. Don't include any sensitive information in task sequence packages such as scripts. Store and implement all sensitive information by using task sequence variables.
 
    - For HTTP communications, select **Create self-signed media certificate**. Then specify the start and expiration date for the certificate.  
    
        > [!NOTE] 
        > If you select this option HTTPS management points will not be available for selection on the **Boot image** page of this wizard.

    - For HTTPS communications, select **Import PKI certificate**. Then specify the certificate to import and its password.  

        For more information about this client certificate that boot images use, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **User device affinity**: To support user-centric management in Configuration Manager, specify how you want the media to associate users with the destination computer. For more information about how OS deployment supports user device affinity, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

        - **Allow user device affinity with auto-approval**: The media automatically associates users with the destination computer. This functionality is based on the actions of the task sequence that deploys the OS. In this scenario, the task sequence creates a relationship between the specified users and destination computer when it deploys the OS to the destination computer.  

        - **Allow user device affinity pending administrator approval**: The media associates users with the destination computer after approval is granted. This functionality is based on the scope of the task sequence that deploys the OS. In this scenario, the task sequence creates a relationship between the specified users and the destination computer, but waits for approval from an administrative user before the OS is deployed.  

        - **Do not allow user device affinity**: The media doesn't associate users with the destination computer. In this scenario, the task sequence doesn't associate users with the destination computer when it deploys the OS.  

7. On the **Task Sequence** page, select the task sequence that runs on the destination computer. Verify the list of content referenced by the task sequence.  

    - **Detect associated application dependencies and add them to this media**: Also add content to the media for application dependencies.  

        > [!TIP]  
        > If you don't see expected application dependencies, deselect and then reselect this option to refresh the list.  

8. On the **Boot image** page, specify the following options:  

    > [!IMPORTANT]  
    > The architecture of the boot image that you distribute must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.  

    - **Boot image**: Select the boot image to start the destination computer.  

    - **Distribution point**: Select the distribution point that has the boot image. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        > Your user account needs at least **Read** permissions to the content library on the distribution point.  

    - **Management point**: Only for *site-based media*, select a management point from a primary site.  

    - **Associated management points**: Only for *dynamic media*, select the primary site management points to use, and a priority order for the initial communication.  

        > [!NOTE]  
        > HTTPS enabled management points will only be displayed when a PKI certificate is specified in the **Security** page of this wizard.  

9. On the **Images** page, specify the following options:  

    - **Image package**: Specify the OS image to use. For more information, see [Manage OS images](../get-started/manage-operating-system-images.md).  

    - **Image index**: If the package contains multiple OS images, specify the index of the image to deploy.  

    - **Distribution point**: Specify the distribution point that has the OS image package. The wizard gets the OS image from the distribution point and writes it to the media.  

10. On the **Select Application** page, select additional applications to add to the prestaged media file.  

11. On the **Select Package** page, select additional packages to add to the prestaged media file.  

12. On the **Select Driver Package** page, select additional driver packages to add to the prestaged media file.  

13. On the **Distribution Points** page, select one or more distribution points from which to get content.  

    Configuration Manager only displays distribution points that have the content. Distribute all of the content associated with the task sequence to at least one distribution point before you continue. After you distribute the content, refresh the distribution point list. Remove any distribution points that you already selected on this page, go to the previous page, and then back to the **Distribution Points** page. Alternatively, restart the wizard. For more information, see [Distribute referenced content](distribute-task-sequence-referenced-content.md) and [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. On the **Customization** page, specify the following options:  

    - Add any variables that the task sequence uses.  

    - **Enable prestart command**: Specify any prestart commands that you want to run before the task sequence runs. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs. For more information, see [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > During media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the **CreateTSMedia.log** file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

        If the prestart command requires any content, select the option to **Include files for the prestart command**.  

15. Complete the wizard.  


## Next steps

[Create an image for an OEM in factory or a local depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
