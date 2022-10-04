---
description: Learn how to validate a new location for a driver update using ValidateNewPackageSource class in Configuration Manager.
title: ValidateNewPackageSource method in class SMS_DriverPackage
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 31ec804c-7dfa-41f5-9bac-2b2368cee254
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ValidateNewPackageSource Method in Class SMS_DriverPackage
The `ValidateNewPackageSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, validates a new location for a driver update.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ValidateNewPackageSource(  
     String PackageSource  
);  
```  

#### Parameters  
 `PackageSource`  
 Data type: `String`  

 Qualifiers: [in]  

 The driver package content to verify.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method is new in the latest version of Configuration Manager. Note that it is the only way to change the package source for an [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object. Most other types of packages can be changed in the console, but not the driver package. The access to this package from the console is restricted.  

 To use this method:  

1.  Manually copy the package files from the old source location to the new location.  

2.  In your application, obtain an [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object for the driver.  

3.  Include a call to `ValidateNewPackageSource` on the package.  

4.  On successful return from the method, have the application change the `StoredPkgPath` property in the package to indicate the new source location.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [RebuildPackage Method in Class SMS_DriverPackage](../../../develop/reference/osd/rebuildpackage-method-in-class-sms_driverpackage.md)
