---
title: "SMS_Driver_Details Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 269d8be5-2786-43e2-9313-555dadcab576
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Driver_Details Server WMI Class
The `SMS_Driver_Details` Windows Management Instrumentation (WMI) class is an embedded class, in Configuration Manager, used by the [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) class to describe the list of drivers that have been added to the boot image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Driver_Details  
{  
      UInt32 ID;  
      String SourcePath;  
};  
```  

## Methods  
 The `SMS_Driver_Details` class does not define any methods.  

## Properties  
 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the driver.  

 `SourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The Universal Naming Convention (UNC) path of driver files.  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application uses this class to create objects that are embedded by [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md). For example, the application can add a driver to a boot image package by adding a reference to the required driver in the `ReferencedDrivers` property of an `SMS_BootImagePackage` object. For more information, see How to add a Windows Driver to a Configuration Manager Boot Image Package.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
