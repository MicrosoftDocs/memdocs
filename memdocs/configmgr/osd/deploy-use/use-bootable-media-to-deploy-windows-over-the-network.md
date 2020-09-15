---
title: Use bootable media to deploy Windows over the network
titleSuffix: Configuration Manager
description: Use bootable media deployments in Configuration Manager to deploy the OS when the destination computer starts.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

Starting in version 2006, bootable media can download cloud-based content. For example, you send a USB key to a user at a remote office to reimage their device. Or an office that has a local PXE server, but you want devices to prioritize cloud services as much as possible. Instead of further taxing the WAN to download large OS deployment content, boot media and PXE deployments can now get content from cloud-based sources. For example, a cloud management gateway (CMG) that you enable to share content.

> [!NOTE]
> The device still needs an intranet connection to the management point.

When the task sequence runs, it downloads content from the cloud-based sources. Review **smsts.log** on the client.

### Prerequisites

- Enable the following client setting in the **Cloud Services** group: **Allow access to cloud distribution point**. Make sure the client setting is deployed to the target clients. For more information, see [About client settings - Cloud services](../../core/clients/deploy/about-client-settings.md#cloud-services).

- For the boundary group that the client is in:

  - Associate the content-enabled CMG or cloud distribution point site systems. For more information, see [Configure a boundary group](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Enable the following option: **Prefer cloud based sources over on-premise sources**. For more information, see [Boundary group options for peer downloads](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribute the content referenced by the task sequence to the content-enabled CMG or cloud distribution point.

## Next steps

[User experiences for OS deployment](../understand/user-experience.md#task-sequence-wizard)
