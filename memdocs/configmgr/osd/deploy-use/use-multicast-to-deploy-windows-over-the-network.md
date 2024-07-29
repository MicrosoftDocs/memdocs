---
title: Use multicast to deploy Windows over the network
titleSuffix: Configuration Manager
description: Use multicast in your Configuration Manager environment so that multiple computers can simultaneously download the OS image.
ms.date: 08/11/2020
ms.service: configuration-manager
ms.subservice: osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Use multicast to deploy Windows over the network with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Multicast is a network optimization method that you can use when multiple clients are likely to download the same OS image at the same time. When you use multicast, multiple computers simultaneously download the OS image as it's multicast by the distribution point. This behavior is instead of each client downloading a copy of the image over a separate connection from the distribution point.

Deploy operating systems over the network by using multicast in the following OS deployment scenarios:

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

Complete the steps in one of these OS deployment scenarios. Then use the following sections to support multicast.

## <a name="BKMK_Configure"></a> Configure distribution points for multicast

To use multicast, configure at least one distribution point to support multicast. For more information, see [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

For a list of ports required to support multicast, see [Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## Prepare an OS image for multicast

You need to configure the OS image to support multicast. For more information, see [Prepare the OS image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="BKMK_Deploy"></a> Deploy the task sequence

Deploy the OS to a target collection. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

## Next steps

[User experiences for OS deployment](../understand/user-experience.md)
