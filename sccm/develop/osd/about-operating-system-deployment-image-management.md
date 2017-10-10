---
title: "OS Deployment Image Management"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: c996a3dc-fff5-4c15-a2ce-a9590969d75esearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Operating System Deployment Image Management
There are several package types that System Center Configuration Manager uses to manage reference computer operating system images.  

 For more information about operating system deployment image management, see [Manage operating system images with System Center Configuration Manager](https://docs.microsoft.com/sccm/osd/get-started/manage-operating-system-images).  

## Reference Computer  

### Operating System Installation  
 The operating system installation package contains all the files necessary to install the desired Windows operating system on a reference computer. In System Center Configuration Manager, they are managed by [SMS_OperatingSystemInstallPackage](../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md). This package does not require a program. The task sequence references the source files as needed.  

### Boot Image  
 An operating system deployment boot image is a Windows Pre-Installation Environment (PE) 2.0 image that is used during the operating system deployment process. In Configuration Manager, boot images are managed by [SMS_BootImagePackage](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md). For more information, see [How to Add a Boot Image from a WIM File in Configuration Manager](../../develop/osd/how-to-add-a-boot-image-from-a-wim-file.md).  

### Driver Packages  
 Driver packages contain Windows device drivers that are not included with the operating system. In Configuration Manager they are managed by [SMS_DriverPackage](../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) objects. For more information, see [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md).  

### Sysprep Package  
 Sysprep is a Windows system presentation tool that facilitates image creation and preparation of an image for deployment to multiple computers. Sysprep is supplied with Windows Vista, but if you are deploying Windows XP or an earlier operating system, you must create an [SMS_Package](../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object package to contain Sysprep and its support files. For more information about creating `SMS_Package` objects, see [How to Create a Package](../../develop/core/servers/configure/how-to-create-a-package.md).

## Target Computer  

### Operating System Image  
 Operating system image packages contain operating system images. In Configuration Manager, they are managed by [SMS_ImagePackage](../../develop/reference/osd/sms_imagepackage-server-wmi-class.md) objects. For more information, see [How to Add an Operating System Image Package in Configuration Manager](../../develop/osd/how-to-add-an-operating-system-image-package-in-configuration-manager.md).  

### Configuration Manager 2007 Client Installation  
 Because every operating system deployment installs the Configuration Manager client, you need to create a package (`SMS_Package`) to install the Configuration Manager client. You can use the package definition file that is included with Configuration Manager for the Configuration Manager client upgrade. For more information about creating a package with a package definition file, see [How to Create a Package by Using a Package Definition File Template](../../develop/core/servers/configure/how-to-create-a-package-by-using-a-package-definition-file-template.md).  

### User State Migration Tool  
 If you are migrating user state from one desktop to another, then you should use the User State Migration Tool (USMT) as your migration tool.  

 In Configuration Manager, you create a package (`SMS_Package`) object to run the USMT on the computer. A package program is not required.  

### Other Packages  
 You will need to create other packages (`SMS_Package`) for the applications you want installed on the target computer.  

## Package Distribution  
 You copy the various package types to distribution points by using the same method that you would use for copying `SMS_Package` package object. For more information, see [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md).  

## See Also  
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)   
 [Operating System Deployment Server WMI Classes](../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [Software Distribution Packages](../../develop/core/servers/configure/software-distribution-packages.md)
