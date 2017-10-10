---
title: "RemoveDriverContent Method"
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
ms.assetid: f1cc53f3-3478-4bee-a48a-81d53ffdb3b2searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# RemoveDriverContent Method in Class SMS_DriverPackage
The `RemoveDriverContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes the specified driver from the driver package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RemoveDriverContent(  
     UInt32 ContentIDs[],  
     Boolean bRefreshDPs  
);  
```  

#### Parameters  
 `ContentIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 The IDs for driver content to remove from the driver package.  

 `bRefreshDPs`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true`, by default, to replicate package changes to the distribution points.  

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
 [RebuildPackage Method in Class SMS_DriverPackage](../../../develop/reference/osd/rebuildpackage-method-in-class-sms_driverpackage.md)   
 [ValidateNewPackageSource Method in Class SMS_DriverPackage](../../../develop/reference/osd/validatenewpackagesource-method-in-class-sms_driverpackage.md)
