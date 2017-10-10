---
title: "VerifyPackage Method"
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
ms.assetid: 143aeb29-3c4d-400b-910f-0783b9ca0c5csearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# VerifyPackage Method in Class SMS_DistributionPoint
The `VerifyPackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, verifies the integrity of all the files in the package by calculating the hash of each file.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 VerifyPackage(  
     string PackageId,  
     string NALPath  
);  
```  

#### Parameters  
 `PackageId`  
 Data type: `String`  

 Qualifiers: `[in]`  

 ID for an existing package.  

 `NALPath`  
 Data type: `String`  

 Qualifiers: `[in]`  

 Network abstraction layer (NAL) path to the distribution point server.  

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
