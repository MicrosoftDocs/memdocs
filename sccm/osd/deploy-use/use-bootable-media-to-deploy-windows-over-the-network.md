---
title: Use bootable media to deploy Windows over the network
titleSuffix: Configuration Manager
description: Use bootable media deployments in System Center Configuration Manager to deploy the operating system when the destination computer starts.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Use bootable media to deploy Windows over the network with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You may deploy the operating system when the destination computer starts using a bootable media deployment. The media contains a pointer to the task sequence, the operating system image, and other required content from the network. When the destination computer starts, the computer retrieves the items referenced in the pointer. With the bootable media free of content, you can update the target without having to replace it on the media.

You may deploy operating systems over the network by using multicast in the following operating system deployment scenarios:

-   [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md)  

Complete the steps in one of the operating system deployment scenarios and then use the following sections to use bootable media to deploy the operating system.  

## Configure deployment settings  
When you use bootable media to start the operating system deployment process, configure the deployment to make the operating system available to the media. You may set this option on the **Deployment Settings** page of the Deploy Software Wizard or in the **Deployment Settings** tab in the properties for the deployment. For the **Make available to the following** setting, configure one of the following:

-   Configuration Manager clients, media, and PXE

-   Only media and PXE

-   Only media and PXE (hidden)

## Create the bootable media
You may specify whether the bootable media is a USB flash drive or CD/DVD set. The computer that starts the media must support the option that you choose as a bootable drive. For more information, see [Create bootable media](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Install the operating system from  bootable media  
Insert the bootable media in a bootable drive on the computer, and then power it on to install the operating system.
