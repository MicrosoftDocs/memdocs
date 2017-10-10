---
title: "CancelDistribution Method"
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
ms.assetid: bfc44693-3266-461f-988a-886333ac9aafsearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CancelDistribution Method in Class SMS_DistributionPoint
The `CancelDistribution` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels a package distribution. If there is a distribution in-progress for the specified package to the specified distribution point, then calling this method will cancel the ongoing distribution and the status of the package distribution will be set to failed for this distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 CancelDistribution(  
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
