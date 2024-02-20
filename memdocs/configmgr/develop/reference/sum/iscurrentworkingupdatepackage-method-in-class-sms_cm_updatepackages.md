---
title: IsCurrentWorkingUpdatePackage Method
titleSuffix: Configuration Manager
description: The IsCurrentWorkingUpdatePackage WMI class method checks whether the update package is the package that setup is currently working on.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 01f3462e-0d03-455d-a05e-375fb8681337
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IsCurrentWorkingUpdatePackage Method in Class SMS_CM_UpdatePackages
The `IsCurrentWorkingUpdatePackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, checks whether the update package is the package that setup is currently working on.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 IsCurrentWorkingUpdatePackage(  
     boolean IsCurrentWorkingUpdatePackage  
);  

```  

#### Parameters  
 `IsCurrentWorkingUpdatePackage`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the update package is the package that setup is currently working on; otherwise, `false`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackages Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackages-server-wmi-class.md)   
