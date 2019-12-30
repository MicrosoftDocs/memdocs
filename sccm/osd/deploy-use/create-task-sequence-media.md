---
title: Create task sequence media
titleSuffix: Configuration Manager
description: Create task sequence media to deploy an OS to a destination computer in your Configuration Manager environment.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Create task sequence media

*Applies to: Configuration Manager (current branch)*

You can use media to capture an OS image from a reference computer or to deploy an OS to a destination computer in your Configuration Manager environment. The media that you create can be a CD, DVD set, or a USB flash drive.  

Media is used mostly to deploy operating systems on destination computers that don't have a network connection or that have a low-bandwidth connection to your Configuration Manager site. However, you can also use media to start an OS deployment outside of an existing Windows OS. This method is useful when there's no existing OS, the OS isn't working, or you want to repartition the hard disk.  

Deployment media includes bootable media, stand-alone media, and prestaged media. The content of the media varies, depending on what type of media that you use. For example, stand-alone media contains the task sequence that deploys the OS. Other types of media retrieve task sequences from the management point.  

> [!IMPORTANT]  
> To create task sequence media, you must be an administrator on the computer where you run the Configuration Manager console. If you're not an administrator, you're prompted for administrator credentials when you start the Create Task Sequence Media wizard.  


## <a name="BKMK_PlanCaptureMedia"></a> Capture media

Capture media allows you to capture an OS image from a reference computer. Capture media contains the boot image that starts the reference computer and the task sequence that captures the OS image.

For more information about how to create capture media, see [Create capture media](/sccm/osd/deploy-use/create-capture-media).  


## <a name="BKMK_PlanBootableMedia"></a> Bootable media

Bootable media contains the following components:

- The boot image
- Optional [prestart commands](/sccm/osd/understand/prestart-commands-for-task-sequence-media) and their required files
- Configuration Manager binaries

When the destination computer starts, it connects to the network and retrieves the task sequence, the OS image, and any other required content from the network. Because the task sequence isn't on the media, you can change the task sequence or content without having to recreate the media.  

> [!IMPORTANT]  
> The packages on bootable media aren't encrypted. Take appropriate security measures, such as adding a password to the media, to make sure that the package contents are secured from unauthorized users.  

For more information about how to create bootable media, [Create bootable media](/sccm/osd/deploy-use/create-bootable-media).  


## <a name="BKMK_PlanPrestagedMedia"></a> Prestaged media

Prestaged media allows you to apply bootable media and an OS image to a hard disk before the provisioning process. The prestaged media is a Windows Image (WIM) file. It can be installed on a bare-metal computer by the manufacturer or at your staging center that's not connected to the production Configuration Manager environment.  

Prestaged media contains the boot image used to start the destination computer and the OS image that's applied to the destination computer. You can also specify applications, packages, and driver packages to include as part of the prestaged media. The task sequence that deploys the OS isn't included in the media. When you deploy a task sequence that uses prestaged media, the client checks the local task sequence cache for valid content first. If the content can't be found or has been revised, the client downloads the content from a distribution point or peer.  

Prestaged media is applied to the hard drive of a new computer before the computer is sent to the end user. When the computer starts for the first time after you've applied the prestaged media, the computer starts in Windows PE. It connects to a management point to locate the task sequence that completes the OS deployment process.  

> [!IMPORTANT]  
> The packages on prestaged media aren't encrypted. Take appropriate security measures, such as adding a password to the media, to make sure that the package contents are secured from unauthorized users.  

For more information about how to create prestaged media, see [Create prestaged media](/sccm/osd/deploy-use/create-prestaged-media).  


## <a name="BKMK_PlanStandaloneMedia"></a> Stand-alone media

Stand-alone media contains everything that's required to deploy the OS. This content includes the task sequence and any other required content. Because everything that's required to deploy the OS is stored on the stand-alone media, the disk space required for stand-alone media is larger than for other types of media.  

For more information about how to create stand-alone media, see [Create stand-alone media](/sccm/osd/deploy-use/create-stand-alone-media).  


## Considerations when using HTTPS

When you configure your management points and distribution points to use HTTPS, create boot media and prestaged media at a primary site, not the central administration site. Also, consider the following point to help you determine whether to configure the media as dynamic or site-based:  

- To configure the media as dynamic media, all primary sites must have the root certificate authority (CA) of the site from which you created the media. You can import the root CA to all primary sites in your hierarchy.  

- When primary sites in your Configuration Manager hierarchy use different root CAs, you must use site-based media at each site.  
