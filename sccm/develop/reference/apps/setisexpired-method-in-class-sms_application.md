---
title: "SetIsExpired Method"
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
ms.assetid: 19057632-e75d-4b1c-ab26-72aeb1da2974searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SetIsExpired Method in Class SMS_Application
The `SetIsExpired` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the expired status of this application.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 SetIsExpired (  
     boolean Expired  
);  
```  

#### Parameters  
 `Expired`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` to set the state to expired, otherwise, `false`. The default value is `true`.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
 [Configuration Manager Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
