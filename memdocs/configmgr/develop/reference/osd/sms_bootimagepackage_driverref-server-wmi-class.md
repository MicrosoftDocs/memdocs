---
title: SMS_BootImagePackage_DriverRef Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents the association between a boot image package and a referenced driver.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a1006a04-8bc9-4e2d-b6e6-7b968208140b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_BootImagePackage_DriverRef Server WMI Class
The `SMS_BootImagePackage_DriverRef` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the association between a boot image package and a referenced driver.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BootImagePackage_DriverRef : SMS_BaseClass  
{  
     SInt32 CI_ID;  
     String PkgID;  
     String SourcePath;  
};  
```  

## Methods  
 The `SMS_BootImagePackage_DriverRef` class doesn't define any methods.  

## Properties  
 `CI_ID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique ID of the configuration item associated with the [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object. This ID is unique only for the site. The default value is 0.  

 `PkgID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key]  

 ID of the boot image package. The default value is "".  

 `SourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Location of the driver content. The default value is "".  

 The value of this property is typically the same as the `ContentSourcePath` property for the associated [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object. However, the value can be different if the original content location isn't available.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  The boot image package is represented by an [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) object. The drivers contained in the package are indicated in the `ReferencedDrivers` property of this object.  

  Your application uses this class to determine what drivers are maintained with the boot image.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_BootImagePackage server WMI class](sms_bootimagepackage-server-wmi-class.md)
