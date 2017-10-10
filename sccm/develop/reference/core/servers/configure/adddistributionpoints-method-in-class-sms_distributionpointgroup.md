---
title: "AddDistributionPoints Method"
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
ms.assetid: a02c595e-31ef-423e-b622-5ae546ea3fa4searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# AddDistributionPoints Method in Class SMS_DistributionPointGroup
The `AddDistributionPoints` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, adds distribution points to the distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 AddDistributionPoints(  
     string DPNALPath[],  
     boolean AddTargetedPackages  
);  
```  

#### Parameters  
 `DPNALPath`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 Distribution point NAL path.  

 `AddTargetedPackages`  
 Data type: `Boolean`  

 Qualifiers: `[in, optional]`  

 `True` if   

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
