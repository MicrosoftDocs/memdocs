---
title: Use multicast to deploy Windows over the network
titleSuffix: Configuration Manager
description: Use multicast in your Configuration Manager environment so that multiple computers can simultaneously download the operating system image.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby



---
# Use multicast to deploy Windows over the network with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Multicast is a network optimization method that you can use in your Configuration Manager environment where multiple clients are likely to download the same operating system image at the same time. When multicast is used, multiple computers simultaneously download the operating system image as it is multicast by the distribution point, rather than having the distribution point send a copy of the data to each client over a separate connection.  

 You can deploy operating systems over the network by using multicast in the following operating system deployment scenarios:  

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

  Complete the steps in one of the operating system deployment scenarios and then use the following sections to support multicast.  

##  <a name="BKMK_Configure"></a> Configure a distribution point to support multicast  
 To use multicast when you   deploy operating systems, you must configure a distribution point to support multicast. For more information, see [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). For a list of ports required to support multicast, see [Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## Prepare an operating system image for multicast deployments  
 To configure the operating system image package to support multicast, see [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Deploy the task sequence  
 Deploy the operating system to a target collection. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).  
