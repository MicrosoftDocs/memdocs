---
title: Scenarios to deploy enterprise operating systems
description: "Learn about several scenarios to deploy enterprise operating systems with System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
caps.latest.revision: 11
author: Dougebyms.author: dougebymanager: angrobe

---
# Scenarios to deploy enterprise operating systems with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
There following operating system deployment scenarios are available in System Center Configuration Manager:  

-   [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md): This scenario upgrades the operating system on computers that currently run Windows 7, Windows 8, Windows 8.1, or Windows 10. The upgrade process retains the applications, settings, and user data on the computer. There are no external dependencies, such as the Windows ADK and this process is faster and more resilient than traditional operating system deployments.  

-   [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md): This scenario partitions and formats (wipes) an existing computer and installs a new operating system on the computer. You can migrate settings and user data after the operating system is installed.  

-   [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md): This scenario  installs an operating system on a new computer. This is a fresh installation of the operating system and does not include any settings or user data migration.  

-   [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md): This scenario installs an operating system on a new computer. Optionally, you can migrate settings and user data from the old computer to the new computer.  

## Things to consider before you deploy operating system images  
 There are certain things that you should consider before you deploy an operating system.  

### Operating system image size  
 The size of an operating system image can be quite large. For example, the image size for Windows 7 is 3 gigabytes (GB) or more. The size of the image and the number of computers that you simultaneously deploy the operating system to affects the network performance and available bandwidth. Ensure that you test the network performance to better gauge the affect that the image deployment might have and the time it takes to complete the deployment. Configuration Manager activities that affect network performance include distributing the image to a distribution point, distributing the image from one site to another, and downloading the image to the Configuration Manager client.  

 Also ensure that you plan for sufficient disk storage space on the distribution points that host the operating system images.  

### Client cache size  
 When Configuration Manager clients download content, they automatically use Background Intelligent Transfer Service (BITS) if it is available. When you deploy a task sequence that installs an operating system, you can set an option on the deployment so that Configuration Manager clients download the full image to a local cache before the task sequence runs.  

 In general, when a Configuration Manager client must download an operating system image (or any other  package), but there is not enough space in the cache, the client checks the other packages in the cache to determine whether deleting any, or all, of the oldest packages will free enough disk space to accommodate the image. If deleting packages does not free enough disk space, the client does not download the image and the deployment fails. This might occur if the cache has a large package that is configured to persist in the cache. If deleting packages does free enough disk space in the cache, the client deletes them, and then downloads the image into the cache.  

 The default cache size on Configuration Manager clients might not be large enough for most operating system image deployments. If you plan to download the full image to the client cache, you must adjust the Configuration Manager client cache size on the destination computers to accommodate the size of the image that you are deploying.  

 For more information, see [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## Task sequence deployments  
 The task sequence that you create can deploy the operating system image on a Configuration Manager client computer in one of the following ways:  

-   Download the image and its content first to the Configuration Manager client cache from a distribution point and then install it.  

-   Install the image and its content immediately from the distribution point.  

-   Install the image and its content as it is required from the distribution point  

 By default, when you create the deployment for the task sequence, the image is downloaded first to the Configuration Manager client cache and then installed. If you select to download the image to the Configuration Manager client cache before you run the image, and the task sequence contains a step to repartition the hard drive, the repartition step fails because partitioning the hard drive erases the contents of the Configuration Manager client cache. If the task sequence must repartition the hard drive, you must run the image installation from the distribution point by using the **Run program from distribution point**  option when you deploy the task sequence.  

 For more information, see [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
