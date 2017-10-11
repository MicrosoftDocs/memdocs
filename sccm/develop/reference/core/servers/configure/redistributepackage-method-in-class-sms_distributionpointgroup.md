---
title: "ReDistributePackage Method"
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
ms.assetid: 0eda3c97-28a6-481c-8af4-6dfbd7942bf7searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ReDistributePackage Method in Class SMS_DistributionPointGroup
The `ReDistributePackage` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, redistributes a package to all of the member distribution points.  

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
 [Application Model Server WMI Classes](../../../../../develop/reference/apps/application-management-server-wmi-classes.md)
