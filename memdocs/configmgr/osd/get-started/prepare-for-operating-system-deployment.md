---
title: Prepare for OS deployment
titleSuffix: Configuration Manager
description: Learn about how to prepare for operating system deployments in Configuration Manager
ms.date: 02/22/2019
ms.service: configuration-manager
ms.subservice: osd
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Prepare for OS deployment in Configuration Manager

*Applies to: Configuration Manager (current branch)*

There are several things you must do in Configuration Manager before you can deploy operating systems. Use the following articles to prepare for OS deployment:  

-   [Manage boot images](manage-boot-images.md)  

-   [Manage OS images](manage-operating-system-images.md)  

-   [Manage OS upgrade packages](manage-operating-system-upgrade-packages.md)  

-   [Manage drivers](manage-drivers.md)  

-   [Manage user state](manage-user-state.md)  

-   [Prepare for unknown computer deployments](prepare-for-unknown-computer-deployments.md)  

-   [Associate users with a destination computer](associate-users-with-a-destination-computer.md)  



### OS image size  

OS images are large in size. For example, the image size for Windows 7 is 3 GB or more. The size of the image and the number of computers to which you simultaneously deploy the OS affects the network performance and available bandwidth. Make sure to test the network performance. Testing the impact better gauges the effect the image deployment might have and the time it takes to complete the deployment. Configuration Manager activities that affect network performance include distributing the image to a distribution point, distributing the image from one site to another, and downloading the image to the client.  

Also make sure that you plan for sufficient disk storage space on the distribution points that host the OS images.  

For more information, see [Additional planning considerations for distribution points](prepare-site-system-roles-for-operating-system-deployments.md#additional-planning-considerations-for-distribution-points).


### Client cache size  

When Configuration Manager clients download content, they automatically use Background Intelligent Transfer Service (BITS), if it's available. When you deploy a task sequence that installs an OS, you can set an option on the deployment so that Configuration Manager clients download the full image to a local cache before the task sequence runs.  

When a Configuration Manager client must download an OS image, but there isn't enough space in the cache, the client can clear space in its cache. It checks the other packages in the cache to determine whether deleting any of the oldest packages will free enough disk space to accommodate the image. If deleting packages doesn't free enough space, the client doesn't download the image, and the deployment fails. This behavior might occur if the cache has a large package that you configure to persist in the cache. If deleting packages does free enough disk space in the cache, the client deletes them, and then downloads the image into the cache.  

The default cache size on Configuration Manager clients might not be large enough for most OS image deployments. If you plan to download the full image to the client cache, adjust the client cache size on the destination computers to accommodate the size of the image that you're deploying.  

For more information, see [Configure the client cache](../../core/clients/manage/configure-client-cache.md).
