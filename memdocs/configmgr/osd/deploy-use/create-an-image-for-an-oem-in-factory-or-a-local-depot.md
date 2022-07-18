---
title: Create an image for an OEM in factory or a local depot
titleSuffix: Configuration Manager
description: Use prestaged media deployments to reduce network traffic while you deploy an OS to a computer that isn't fully provisioned.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create an image for an OEM in factory or a local depot with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Prestaged media deployments in Configuration Manager let you deploy an OS to a computer that isn't fully provisioned. The prestaged media is a Windows image (WIM) file. The manufacturer (OEM) can install it on a bare-metal computer, or you can use it in a staging center that's separate from your production environment.

This method of deployment can reduce network traffic because the boot image and OS image are already on the destination computer. You can specify applications, packages, and driver packages to also include in the prestaged media. After it installs the OS on the computer, the task sequence first checks the prestaged cache for applications, packages, or driver packages. If it can't find the necessary content, or there is a newer revision available online, the task sequence downloads the content from a distribution point.

Use prestaged media in the following OS deployment scenarios:

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)

Complete the steps in one of these OS deployment scenarios. Then use the following sections to prepare for and create the prestaged media.

## Configure deployment settings

On the **Deployment Settings** page of the deployment, for the **Make available to the following** setting, select one of the following options:

- Configuration Manager clients, media, and PXE

- Only media and PXE

- Only media and PXE (hidden)

## Create the prestaged media

Create the prestaged media file to send to the OEM or your local depot. For more information, see [Create prestaged media with Configuration Manager](create-prestaged-media.md).

## Send the prestaged media file

Send the media to the OEM or your local depot to prestage on the computers. They apply the image file to a formatted hard disk on the computer.

## Deliver the computer

When you deliver the computer to a user, and turn it on for the first time:

1. The computer starts with the prestaged boot image.

1. It checks a hash on the prestaged media to make sure it's valid.

1. The computer connects to the management point for available task sequences to complete the process.

## Next steps

[User experiences for OS deployment](../understand/user-experience.md)
