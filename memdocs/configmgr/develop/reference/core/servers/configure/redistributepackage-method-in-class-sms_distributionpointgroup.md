---
title: ReDistributePackage Method
titleSuffix: Configuration Manager
description: In Configuration Manager, The ReDistributePackage WMI class method redistributes a package to all of the member distribution points.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0eda3c97-28a6-481c-8af4-6dfbd7942bf7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ReDistributePackage Method in Class SMS_DistributionPointGroup
The `ReDistributePackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, redistributes a package to all of the member distribution points.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 ReDistributePackage (  
     string PackageID  
);  
```  

#### Parameters  
 `PackageID`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
