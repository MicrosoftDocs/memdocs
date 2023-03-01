---
title: RebuildPackage method in class SMS_DriverPackage
titleSuffix: Configuration Manager
description: The RebuildPackage Windows Management Instrumentation (WMI) class method, in Configuration Manager, restores the contents for the driver package.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ea311e8c-5ad5-4c0c-882f-eeb8e74ba0f0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RebuildPackage Method in Class SMS_DriverPackage
The `RebuildPackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, restores the contents for the driver package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RebuildPackage(  
     String ContentSourcePath  
);  
```  

#### Parameters  
 `ContentSourcePath`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 Source path where the content files are located.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [AddDriverContent Method in Class SMS_DriverPackage](../../../develop/reference/osd/adddrivercontent-method-in-class-sms_driverpackage.md)   
 [RemoveDriverContent Method in Class SMS_DriverPackage](../../../develop/reference/osd/removedrivercontent-method-in-class-sms_driverpackage.md)   
 [ValidateNewPackageSource Method in Class SMS_DriverPackage](../../../develop/reference/osd/validatenewpackagesource-method-in-class-sms_driverpackage.md)
