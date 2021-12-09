---
title: Refresh an existing computer's OS
titleSuffix: Configuration Manager
description: You can use several methods in Configuration Manager to partition and format an existing computer and install a new OS on the computer.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Refresh an existing computer with a new version of Windows

*Applies to: Configuration Manager (current branch)*

Use Configuration Manager to partition and format an existing computer and then install a new OS. This process is sometimes called *reimaging* or *wipe and load*. For this scenario, choose from many different deployment methods, such as PXE, bootable media, or Software Center. You can also use a state migration point to store settings, and then restore them to the new OS.

To choose the right OS deployment scenario, see [Scenarios to deploy enterprise operating systems](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="BKMK_Plan"></a> Plan  

### Plan for and implement infrastructure requirements

There are several infrastructure requirements that must be in place before you can deploy an OS. Some of these requirements include the Windows ADK, the User State Migration Tool (USMT), and Windows Deployment Services (WDS). For more information, see [Infrastructure requirements for OS deployment](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### Install a state migration point

If you want to capture settings from an existing computer, and then restore the settings to the new OS, consider using a state migration point. For more information, see [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#state-migration-point).  

## <a name="BKMK_Configure"></a> Configure  

### Prepare a boot image

Boot images start a computer in a Windows PE environment. Windows PE is a minimal OS with limited components and services. From Windows PE, Configuration Manager can then install a full Windows OS on the computer.

For more information, see the following articles:

- [Manage boot images](../get-started/manage-boot-images.md)

- [Customize boot images](../get-started/customize-boot-images.md)

- [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### Prepare an OS image

The OS image contains the files necessary to install the OS on the destination computer.

For more information, see the following articles:

- [Manage OS images](../get-started/manage-operating-system-images.md)

- [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### Create a task sequence to deploy an OS

Use a task sequence to automate the installation of the OS. Depending on the deployment method that you choose, there might be additional considerations for the task sequence.

For more information, see the following articles:

- [Create a task sequence to install an OS](create-a-task-sequence-to-install-an-operating-system.md)

- [Manage user state](../get-started/manage-user-state.md)

## <a name="BKMK_Deploy"></a> Deploy

- Use one of the following deployment methods to deploy the OS:  

  - [Use PXE to deploy Windows over the network](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Use multicast to deploy Windows over the network](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Create an image for an OEM in factory or a local depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Use bootable media to deploy Windows over the network](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md)  

## Monitor  

For more information, see [Monitor OS deployments](monitor-operating-system-deployments.md).  

> [!Note]
> When you reimage a UEFI device, Windows Boot Manager creates a new entry in the boot loader. This behavior is most noticeable when you repeatedly reimage a device, such as in a test environment or a student lab. It generally doesn't impact the performance or usage of the device. If the list gets too large, some specific hardware devices may encounter functional issues. For example, not booting to an external USB drive, or not able to select the current boot entry from the list. Use the Windows **bcdedit** command to clear unused boot entries. For more information, see [BCDEdit /deletevalue](/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->