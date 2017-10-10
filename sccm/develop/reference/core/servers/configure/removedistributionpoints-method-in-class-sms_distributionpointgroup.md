---
title: "RemoveDistributionPoints Method"
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
ms.assetid: 9cfacf13-1d30-4a0c-9453-aaa3e9aa677bsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# RemoveDistributionPoints Method in Class SMS_DistributionPointGroup
The `RemoveDistributionPoints` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, removes distribution points from this distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemoveDistributionPoints(  
     string DPNALPath[],  
     boolean RemoveTargetedPackages  
);  
```  

#### Parameters  
 `DPNALPath`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 Distribution point NAL path.  

 `RemoveTargetedPackages`  
 Data type: `Boolean`  

 Qualifiers: `[in, optional]`  

 `true` if …  The default value is `false`.  

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
