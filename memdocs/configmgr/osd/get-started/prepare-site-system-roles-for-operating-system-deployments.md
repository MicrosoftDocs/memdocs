---
title: Prepare site system roles for OSD
titleSuffix: Configuration Manager
description: Configure the site system roles before you deploy operating systems in Configuration Manager.
ms.date: 10/01/2021
ms.service: configuration-manager
ms.subservice: osd
ms.topic: install-set-up-deploy
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Prepare site system roles for OS deployments with Configuration Manager

*Applies to: Configuration Manager (current branch)*

To deploy operating systems in Configuration Manager, first prepare the following site system roles that require specific configurations and considerations.

## Distribution points

The distribution point site system role hosts source files for clients to download. This content is for applications, software updates, OS images, boot images, and driver packages. Control content distribution by using bandwidth, throttling, and scheduling options.

It's important that you have enough distribution points to support the deployment of operating systems to computers. It's also important that you plan for the placement of these distribution points in your hierarchy. For more information, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). This article includes more planning considerations for distribution points specific to OS deployment.

### Additional planning considerations for distribution points

#### How can I prevent unwanted OS deployments?

Configuration Manager doesn't distinguish site servers from other destination computers in a collection. If you deploy a required task sequence to a collection that includes a site server, it runs the task sequence the same way as any other computer in the collection. Make sure that your OS deployment uses a collection that includes the intended clients.

Manage the behavior for high-risk task sequence deployments. A high-risk deployment automatically installs on a client and has the potential to cause unwanted results. For example, a task sequence with a purpose of required that deploys an OS. To reduce the risk of an unwanted high-risk deployment, configure deployment verification settings. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

#### How many computers can receive an OS image at one time from a single distribution point?

To estimate how many distribution points you need, consider the following variables:

- The processing speed of the distribution point
- The disk speed of the distribution point
- The available bandwidth on the network
- The size of the image package

For example, if you don't consider any other server resource factors, the maximum number of computers that can process a 4-GB image package in one hour on a 100-megabit/sec Ethernet network is 11 computers. 

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`

If you must deploy an OS to a specific number of computers within a specific time frame, distribute the image to an appropriate number of distribution points.

#### Can I deploy an OS to a distribution point?

You can deploy an OS to a distribution point, but the OS image must be received from a different distribution point.

### Configuring distribution points to accept PXE requests

To deploy operating systems to Configuration Manager clients that make PXE boot requests, configure one or more distribution points to accept PXE requests. Once you configure the distribution point, it responds to PXE boot requests and determines the appropriate deployment action to take. For more information, see [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

### Customize the RamDisk TFTP block and window sizes on PXE-enabled distribution points

You can customize the RamDisk TFTP block and window sizes for PXE-enabled distribution points. If you've customized your network, a large block or window size could cause the boot image download to fail with a time-out error. The RamDisk TFTP block and window size customizations allow you to optimize TFTP traffic when using PXE to meet your specific network requirements. To determine what configuration is most efficient, test the customized settings in your environment.

- **TFTP block size**: The block size is the size of the data packets that the server sends to the client that is downloading the file. A larger block size allows the server to send fewer packets, so there are fewer round-trip delays between the server and the client. However, a large block size leads to fragmented packets, which most PXE client implementations don't support.

- **TFTP window size**: TFTP requires an acknowledgment (ACK) packet for each block of data that is sent. The server doesn't send the next block in the sequence until it receives the ACK packet for the previous block. TFTP windowing enables you to define how many data blocks it takes to fill a window. The server sends the data blocks back-to-back until the window is filled, and then the client sends an ACK packet. If you increase this window size, it reduces the number of round-trip delays between the client and server, and it decreases the overall required time to download a boot image.

#### Modify the RamDisk TFTP window size

To customize the RamDisk TFTP window size, add the following registry key on PXE-enabled distribution points:

- **Location**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`
- **Name**: RamDiskTFTPWindowSize
- **Type**: REG_DWORD
- **Value**: (customized window size)
  The default value is `1` (one data block fills the window).

#### Modify the RamDisk TFTP block size

To customize the RamDisk TFTP window size, add the following registry key on PXE-enabled distribution points:

- **Location**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`
- **Name**: RamDiskTFTPBlockSize
- **Type**: REG_DWORD
- **Value**: (customized block size)
  The default value is `4096`.

> [!NOTE]
> Both Windows Deployment Services and the Configuration Manager PXE responder service support these TFTP configurations.

### Configure distribution points to support multicast

Multicast is a network optimization method. Use it on distribution points when multiple clients are likely to download the same OS image at the same time. When you use multicast, multiple computers can simultaneously download the OS image as it's multicast by the distribution point. Without multicast, the distribution point sends a copy of the data to each client over a separate connection. For more information, see [Use multicast to deploy Windows over the network](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Before you deploy the OS, configure a distribution point to support multicast. For more information, see [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

## State migration point

The state migration point stores user state data that USMT captures on one computer, and then restores on another computer. However, when you capture user settings for an OS deployment on the same computer, such as a deployment where you refresh Windows on the destination computer, you can choose whether to store the data on the same computer by using hard-links or use a state migration point. For some computer deployments, when you create the state store, Configuration Manager automatically creates an association between the state store and the destination computer. As you plan for the state migration point, consider the following factors:

### User state size

The size of the user state directly affects disk storage on the state migration point and network performance during the migration. Consider the size of the user state and the number of computers to migrate. Consider also what settings to migrate from the computer. For example, if the **My Documents** folder is already backed up to a server, then perhaps you don't have to migrate it as part of the image deployment. Avoiding unnecessary migrations keeps the overall size of the user state smaller, and decreases the effect it would otherwise have on network performance and disk storage on the state migration point.

### User State Migration Tool

To capture and restore the user state during the deployment of the operating systems, use a User State Migration Tool (USMT) package that points to the USMT source files. Configuration Manager automatically creates this package in the Configuration Manager console in **Software Library** > **Application Management** > **Packages**. Configuration Manager uses USMT to capture the user state from one OS and then restore it to another. The Windows Assessment and Deployment Kit (ADK) for Windows includes USMT.

For a description of different migration scenarios for USMT, see [Common migration scenarios](/windows/deployment/usmt/usmt-common-migration-scenarios) in the Windows documentation.

### Retention policy

When you configure the state migration point, specify the length of time to keep the user state data that it stores. The length of time to keep the data on the state migration point depends on two considerations:

- The effect that the stored data has on disk storage.

- The potential requirement to keep the data for a time in case you must migrate the data again.

State migration occurs in two phases: capturing the data, and restoring the data. When you capture data, the user state data is collected and saved to the state migration point. When you restore the data, the user state data is retrieved from the state migration point, written to the destination computer, and then the **Release State Store** task sequence step releases the stored data. When the data is released, the retention timer starts. If you select the option to delete migrated data immediately, the user state data is deleted as soon as it's released. If you select the option to keep the data for a certain period of time, the data is deleted when that period of time elapses after the state data is released. The longer you set the retention period, the more disk space you're likely to require.

### Select drive to store user state migration data

When you configure the state migration point, specify the drive on the server to store the user state migration data. You select a drive from a fixed list of drives. However, some of these drives might represent non-writable drives, such as the CD drive, or a non-network share drive. Some drive letters might not be mapped to any drives on the computer. Specify a writable, shared drive when you configure the state migration point.

### Configure a state migration point

Use the following methods to configure a state migration point to store the user state data:

- Use the **Create Site System Server Wizard** to create a new site system server for the state migration point.

- Use the **Add Site System Roles Wizard** to add a state migration point to an existing server.

When you use these wizards, you're prompted to provide the following information for the state migration point:

- The folders to store the user state data.

- The maximum number of clients that can store data on the state migration point.

- The minimum free space for the state migration point to store user state data.

- The deletion policy for the role. Either specify that the user state data is deleted immediately after it's restored on a computer, or after a specific number of days after the user data is restored on a computer.

- Whether the state migration point responds only to requests to restore user state data. When you enable this option, you can't use the state migration point to store user state data.

For the steps to install a site system role, see [Add site system roles](../../core/servers/deploy/configure/add-site-system-roles.md).

## Next steps

[Prepare for OS deployment](prepare-for-operating-system-deployment.md)
