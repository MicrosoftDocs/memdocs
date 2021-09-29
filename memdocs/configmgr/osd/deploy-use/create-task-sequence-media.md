---
title: Create task sequence media
titleSuffix: Configuration Manager
description: Create task sequence media to deploy an OS to a destination computer in your Configuration Manager environment.
ms.date: 07/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create task sequence media

*Applies to: Configuration Manager (current branch)*

You can use media to capture an OS image from a reference computer or to deploy an OS to a destination computer in your Configuration Manager environment. The media that you create can be a CD, DVD set, or a USB flash drive.

Media is used mostly to deploy an OS on computers that don't have a network connection or that have a low-bandwidth connection to the site. However, you can also use media to start an OS deployment outside of an existing Windows OS. This method is useful when there's no OS, the OS isn't working, or you want to repartition the disk.

Deployment media includes bootable media, standalone media, and prestaged media. The content of the media varies, depending on what type of media that you use. For example, standalone media contains the task sequence that deploys the OS. Other types of media retrieve task sequences from the management point.

> [!IMPORTANT]
> To create task sequence media, you must be an administrator on the computer where you run the Configuration Manager console. If you're not an administrator, you're prompted for administrator credentials when you start the Create Task Sequence Media wizard.

## <a name="BKMK_PlanCaptureMedia"></a> Capture media

Capture media allows you to capture an OS image from a reference computer. Capture media contains the boot image that starts the reference computer and the task sequence that captures the OS image.

## <a name="BKMK_PlanBootableMedia"></a> Bootable media

Bootable media contains the following components:

- The boot image
- Optional [prestart commands](../understand/prestart-commands-for-task-sequence-media.md) and their required files
- Configuration Manager binaries

When the destination computer starts, it connects to the network and retrieves the task sequence, the OS image, and any other required content from the network. Because the task sequence isn't on the media, you can change the task sequence or content without having to recreate the media.  

> [!IMPORTANT]  
> The packages on bootable media aren't encrypted. Take appropriate security measures, such as adding a password to the media, to make sure that the package contents are secured from unauthorized users.  

Starting in version 2006, bootable media can download cloud-based content. The device still needs an intranet connection to the management point. It can get content from a content-enabled cloud management gateway (CMG).<!--6209223--> For more information, see [Bootable media support for cloud-based content](deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content).

## <a name="BKMK_PlanPrestagedMedia"></a> Prestaged media

Prestaged media allows you to apply bootable media and an OS image to a hard disk before the provisioning process. The prestaged media is a Windows Image (WIM) file. The manufacturer can install it to the bare-metal computer during their build process. Or you can use it in a staging center that's not connected to the production Configuration Manager environment.

Prestaged media contains the boot image used to start the destination computer and the OS image that's applied to the destination computer. You can also specify applications, packages, and driver packages to include as part of the prestaged media. The task sequence that deploys the OS isn't included in the media. When you deploy a task sequence that uses prestaged media, the client checks the local task sequence cache for valid content first. If the content can't be found or has been revised, the client downloads the content from a distribution point or peer.  

You apply prestaged media to the hard drive of a new computer before you send the computer to the user. When the computer starts for the first time after you've applied the prestaged media, the computer starts in Windows PE. It connects to a management point to locate the task sequence that completes the OS deployment process.  

> [!IMPORTANT]
> The packages on prestaged media aren't encrypted. Take appropriate security measures, such as adding a password to the media, to make sure that the package contents are secured from unauthorized users.

## <a name="BKMK_PlanStandaloneMedia"></a> Standalone media

Standalone media contains everything that's required to deploy the OS. This content includes the task sequence and any other required content. Because everything is on the media, the required disk space is larger than for other types of media.

## Considerations when using HTTPS

When you configure your management points and distribution points to use HTTPS, create boot media and prestaged media at a primary site, not the central administration site. Also, consider the following point to help you determine whether to configure the media as dynamic or site-based:  

- To configure the media as dynamic media, all primary sites must have the root certificate authority (CA) of the site from which you created the media. You can import the root CA to all primary sites in your hierarchy.  

- When primary sites in your Configuration Manager hierarchy use different root CAs, you must use site-based media at each site.  

## Next steps

- [Create capture media](create-capture-media.md)

- [Create bootable media](create-bootable-media.md)

- [Create prestaged media](create-prestaged-media.md)

- [Create standalone media](create-stand-alone-media.md)
