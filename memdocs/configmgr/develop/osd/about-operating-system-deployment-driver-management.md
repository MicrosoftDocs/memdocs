---
title: OS Deployment Driver Management
description: In Configuration Manager, the driver catalog helps manage the cost and complexity of deploying an operating system in an environment that contains different types of computers and devices.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 789d981f-d0c5-447b-9d93-24d2e0eef5f0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Operating System Deployment Driver Management
In Configuration Manager, the driver catalog helps manage the cost and complexity of deploying an operating system in an environment that contains different types of computers and devices. By storing device drivers in the driver catalog and not with each individual operating system image, the number of operating system images that is needed is greatly reduced. For more information about the driver catalog, see [Manage drivers](../../osd/get-started/manage-drivers.md).  

> [!NOTE]
>  Before a driver can be used, it must be added to a driver package. For more information, see [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md).  

## Driver Catalog Management  
 With the Configuration Manager Operating System Deployment server Windows Management Instrumentation (WMI) classes you can manage the following:  

-   Driver import  

-   Driver packages  

-   Boot images  

-   Supported platforms  

### Driver Import  
 Using the [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) import methods, you can import the Windows drivers described by .inf and Txtsetup.oem files into the driver catalog. For more information, see [How to Import a Windows Driver Described by an INF File into Configuration Manager](../../develop/osd/how-to-import-a-windows-driver-described-by-an-inf-file.md) and [How to Import a Windows Driver Described by an OEM File into Configuration Manager](../../develop/osd/how-to-import-a-windows-driver-described-by-a-txtsetup-oem-file.md).  

 Before a driver can be used, it must be enabled. For more information, see [How to Enable or Disable a Windows Driver in Configuration Manager](../../develop/osd/how-to-enable-or-disable-a-windows-driver.md).  

### Driver Packages  
 Driver packages contain one or more Windows drivers. A driver package is an `SMS_DriverPackage` object and is distributed in the same way as an `SMS_Package` package. They both derive from [SMS_PackageBaseClass](../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 For more information about creating a driver package, see [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md).  

### Boot Images  
 Windows device drivers that have been imported into the driver catalog can be added to one or more boot images. Boot images are stored in [SMS_BootImagePackage](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) objects. In an `SMS_BootImagePackage` object, Windows drivers are kept in an array of referenced drivers. For more information, see [How to add a Windows Driver to a Configuration Manager Boot Image Package](../../develop/osd/how-to-add-a-windows-driver-to-a-configuration-manager-boot-image-package.md)  

### Supported Platforms  
 Windows drivers can be configured to support specific platforms. The supported platforms are stored in the driver package XML. For more information, see [How to Specify The Supported Platforms for a Driver](../../develop/osd/how-to-specify-the-supported-platforms-for-a-driver.md).  

### Driver Categories  
 You can associate categories with Windows device drivers. For more information, see [How to Add a Category to a Windows Driver](../../develop/osd/how-to-add-a-category-to-a-windows-driver.md)
