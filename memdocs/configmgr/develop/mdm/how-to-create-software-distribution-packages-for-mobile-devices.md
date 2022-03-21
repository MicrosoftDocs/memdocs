---
title: "Create Software Distribution Packages for Mobile Devices"
titleSuffix: "Configuration Manager"
description: How to Create Software Distribution Packages, Programs, and Advertisements for Mobile Devices
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 3becb7a9-cf6b-432b-85e7-a0087df0dbb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create Software Distribution Packages, Programs, and Advertisements for Mobile Devices
Configuration Manager device management enables mobile device software distribution to mobile devices. Packages, programs, and advertisements for mobile devices are much the same as those for computer clients. For detailed information about creating packages, programs and advertisements, see the following topics:  

-   [How to Create a Package](../../develop/core/servers/configure/how-to-create-a-package.md)  

-   [How to Create a Program](../../develop/core/servers/configure/how-to-create-a-program.md)  

-   [How to Create an Advertisement](../../develop/core/servers/configure/how-to-create-an-advertisement.md)  

> [!IMPORTANT]
> This article only applies to the mobile device legacy client.

## Packages  
 Packages for mobile devices in Configuration Manager generally represent a software application to be installed on a mobile device, but they might also contain individual files, updates, or even an individual command.  

### Configuration Packages  
 Configuration packages are packages specifically for mobile devices. These packages contain one or more configuration items. Configuration items are collections of settings for one or more mobile device platforms.  

## Programs  
 Programs for mobile devices in Configuration Manager are commands that are distributed with a Configuration Manager package that tell a mobile device client what should occur when the package is received.  

## Advertisements  
 Advertisements for mobile devices in Configuration Manager allow mobile devices to download and install available packages. Advertisements for mobile devices are much the same as advertisements for computer clients. Mobile device advertisement programs will not run on desktop computers and computer advertisement programs will not run on mobile devices. Advertisements can be created in two ways, one for each type of package that can be advertised to mobile devices. The following advertisements can be sent to mobile devices:  

-   Advertisements for configuration packages for mobile devices  

-   Advertisements for software distribution packages for mobile devices  

### Advertisements for Configuration Packages  
 Configuration packages are packages specifically for mobile devices. These packages contain one or more configuration items. Configuration items are collections of settings for one or more mobile device platforms.  

### Advertisements for Software Distribution Packages  
 Advertisements for mobile devices are identical to software distribution packages for computer clients except that they target mobile devices and contain content that is appropriate for mobile devices.  

## See also

- [Software distribution overview](../core/servers/configure/software-distribution-overview.md)
- [About deployments](../core/servers/configure/about-software-distribution-deployments.md)
