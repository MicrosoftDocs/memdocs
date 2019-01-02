---
title: Create prestaged media
titleSuffix: Configuration Manager
description: Create prestaged media in System Center Configuration Manager to simplify deployment of Windows in several scenarios.
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create prestaged media with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Prestaged media in System Center Configuration Manager is a Windows Imaging Format (WIM) file that can be installed on a bare-metal computer by the manufacturer or at an enterprise staging center that is not connected to the Configuration Manager environment.  
Prestaged media contains the boot image used to start the destination computer and the operating system image that is applied to the destination computer. You can also specify applications, packages, and driver packages to include as part of the prestaged media. The task sequence that deploys the operating system is not included in the media. Prestaged media is applied to the hard drive of a new computer before the computer is sent to the end user. Use prestaged media for the following operating system deployment scenarios:  

- [Create an image for an OEM in factory or a local depot](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Deploy Windows to Go](deploy-windows-to-go.md)  

  When the computer starts for the first time after the prestaged media has been applied, the computer boots to Windows PE and connects to a management point to locate the task sequence that completes the operating system deployment process. You can specify applications, packages, and driver packages to include as part of the prestaged media. When you deploy a task sequence that uses prestaged media, the wizard checks the local task sequence cache for valid content first, and if the content cannot be found or has been revised, the wizard downloads the content from the distribution point.  

##  <a name="BKMK_CreatePrestagedMedia"></a> How to Create Prestaged Media  
 Before you create prestaged media by using the Create Task Sequence Media Wizard, be sure that all the following conditions are met:  

|Task|Description|  
|----------|-----------------|  
|Boot image|Consider the following about the boot image that you will use in the task sequence to deploy the operating system:<br /><br /> -   The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.<br />-   Ensure that the boot image contains the network and mass storage drivers that are required to provision the destination computer.|  
|Create a task sequence to deploy an operating system|As part of the prestaged media, you must specify the task sequence to deploy the operating system.<br /><br /> -   For the steps to create a new task sequence, see [Create a task sequence to install an operating system](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />-   For more information about task sequences, see [Manage task sequences to automate tasks](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Distribute all content associated with the task sequence|You must distribute to at least one distribution point all content that is required by the task sequence. This includes the boot image, operating system image, and other associated files. The wizard gathers the information from the distribution point when it creates the stand-alone media. You must have **Read** access rights to the content library on that distribution point.  For details, see [About the content library](../../core/plan-design/hierarchy/the-content-library.md).|  
|Hard drive on the destination computer|The hard drive of the destination computer must be formatted before the pre-staged media is staged onto the hard drive of the computer. If the hard drive is not formatted when the media is applied, the task sequence that deploys the operating system will fail when it attempts to start the destination computer.|  

> [!NOTE]  
>  The Create Task Sequence Media Wizard sets the following task sequence variable condition on the media: **_SMSTSMediaType = OEMMedia**. You can use this condition in your task sequence.  

 Use the following procedure to create prestaged media.  

#### To create prestaged media  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence Media** to start the Create Task Sequence Media Wizard.  

4.  On the **Select Media Type** page, specify the following information, and then click **Next**.  

    -   Select **Prestaged media**.  

    -   Optionally, if you want to allow the operating system to be deployed without requiring user input, select **Allow unattended operating system deployment**. When you select this option the user is not prompted for network configuration information or for optional task sequences. However, the user is still prompted for a password if the media is configured for password protection.  

5.  On the **Media Management** page, specify the following information, and then click **Next**.  

    -   Select **Dynamic media** if you want to allow a management point to redirect the media to another management point, based on the client location in the site boundaries.  

    -   Select **Site-based media** if you want the media to contact only the specified management point.  

6.  On the **Media Properties**  page, specify the following information, and then click **Next**.  

    -   **Created by**: Specify who created the media.  

    -   **Version**: Specify the version number of the media.  

    -   **Comment**: Specify a unique description of what the media is used for.  

    -   **Media file**: Specify the name and path of the output files. The wizard writes the output files to this location. For example: **\\\servername\folder\outputfile.wim**  

7.  On the **Security** page, specify the following information, and then click **Next**.  

    -   Select the **Enable unknown computer support** check box to allow the media to deploy an operating system to a computer that is not managed by Configuration Manager. There is no record of these computers in the Configuration Manager database.  For more information, see [Prepare for unknown computer deployments](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Select the **Protect the media with a password** check box and enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the prestaged media.  

        > [!IMPORTANT]  
        >  As a security best practice, always assign a password to help protect the prestaged media.  

    -   For HTTP communications, select **Create self-signed media certificate**, and then specify the start and expiration date for the certificate.  

    -   For HTTPS communications, select **Import PKI certificate**, and then specify the certificate to import and its password.  

         For more information about this client certificate that is used for boot images, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **User Device Affinity**: To support user-centric management in Configuration Manager, specify how you want the media to associate users with the destination computer. For more information about how operating system deployment supports user device affinity, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

        -   Specify **Allow user device affinity with auto-approval** if you want the media to automatically associate users with the destination computer. This functionality is based on the actions of the task sequence that deploys the operating system. In this scenario, the task sequence creates a relationship between the specified users and destination computer when it deploys the operating system to the destination computer.  

        -   Specify **Allow user device affinity pending administrator approval** if you want the media to associate users with the destination computer after approval is granted. This functionality is based on the scope of the task sequence that deploys the operating system. In this scenario, the task sequence creates a relationship between the specified users and the destination computer, but waits for approval from an administrative user before the operating system is deployed.  

        -   Specify **Do not allow user device affinity** if you do not want the media to associate users with the destination computer. In this scenario, the task sequence does not associate users with the destination computer when it deploys the operating system.  

8.  On the **Task Sequence** page, specify the task sequence that will run on the destination computer. The content referenced by the task sequence is displayed in **This task sequence references the following content**. Verify that the content,   and then click **Next**.  

9. On the **Boot image** page, specify the following information, and then click **Next**.  

    > [!IMPORTANT]  
    >  The architecture of the boot image that is distributed must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.  

    -   In the **Boot image** box, specify the boot image to start the destination computer. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

    -   In the **Distribution point** box, specify the distribution point where the boot image resides. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        >  You must have **Read** access rights to the content library on the distribution point. For more information, see [About the content library](../../core/plan-design/hierarchy/the-content-library.md).  

    -   If you selected **Site-based media** on the **Media Management** page of the wizard, in the **Management point** box, specify a management point from a primary site.  

    -   If selected **Dynamic media** on the **Media Management** page of the wizard, in the **Associated management points** box, specify the primary site management points to use and a priority order for the initial communications.  

10. On the **Images** page, specify the following information, and then click **Next**.  

    -   In the **Image package** box, specify the operating system image. For more information, see [Manage operating system images](../get-started/manage-operating-system-images.md).  

    -   If the package contains multiple operating system images, in the **Image index** box, specify the image to deploy.  

    -   In the **Distribution point** box, specify the distribution point where the operating system image package resides. The wizard retrieves the operating system image from the distribution point and writes it to the media.  

11. On the **Customization** page, specify the following information, and then click **Next**.  

    -   Specify the variables that the task sequence uses to deploy the operating system.  

    -   Specify any prestart commands that you want to run before the task sequence runs. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs to install the operating system. For more information about prestart commands for media, see the [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  During task sequence media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the CreateTSMedia.log log file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

12. Complete the wizard.  

## Next steps
[Scenarios to deploy enterprise operating systems](scenarios-to-deploy-enterprise-operating-systems.md)
