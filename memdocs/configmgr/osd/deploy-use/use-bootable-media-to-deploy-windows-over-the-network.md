---
title: Use bootable media to deploy Windows over the network
titleSuffix: Configuration Manager
description: Use bootable media deployments in Configuration Manager to deploy the OS when the destination computer starts.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Use bootable media to deploy Windows over the network with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Bootable media only includes the boot image and a pointer to the task sequence. It downloads the OS image and other referenced content from the network. Since the bootable media doesn't contain much content, you can update the task sequence and most content without having to replace the media.

Deploy operating systems over the network with boot media in the following scenarios:

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)

Complete the steps in one of the OS deployment scenarios and then use the following sections to use bootable media to deploy the OS.

## Configure deployment settings

When you use bootable media to start the OS deployment process, configure the task sequence deployment to make the OS available to the media. Set this option on the **Deployment Settings** page of the deployment. For the **Make available to the following** setting, select one of the following options:

- Configuration Manager clients, media, and PXE

- Only media and PXE

- Only media and PXE (hidden)

For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

## Create the bootable media

When you create bootable media, specify whether it's a USB flash drive or CD/DVD set. The computer that starts the media must support the option that you choose as a bootable drive. For more information, see [Create bootable media](create-bootable-media.md).

## <a name="BKMK_Deploy"></a> Install the OS from bootable media

To install the OS, insert the bootable media, and then power on the computer.

## Support for cloud-based content

<!--6209223-->

Starting in version 2006, bootable media can download cloud-based content. For example, you send a USB key to a user at a remote office to reimage their device. Or an office that has a local PXE server, but you want devices to prioritize cloud services as much as possible. Instead of further taxing the WAN to download large OS deployment content, boot media and PXE deployments can now get content from cloud-based sources.

For more information, see [Bootable media support for cloud-based content](deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content).

## Next steps

[User experiences for OS deployment](../understand/user-experience.md#task-sequence-wizard)
