---
title: "SetEnforcement Method"
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
ms.assetid: 56815dfb-89f5-4e32-bbb7-d654daa044dfsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SetEnforcement Method in Class SMS_ConfigurationItem
The `SetEnforcement` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the enforcement and the enforcement date for a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetEnforcement(  
     Boolean Enforced,  
     DateTime EffectiveDate  
);  
```  

#### Parameters  
 `Enforced`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if policy enforcement is enabled.  

 `EffectiveDate`  
 Data type: `DateTime`  

 Qualifiers: [in]  

 The date and time, in Coordinated Universal Time (UTC), when the configuration item is compliant.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)
