---
title: "Close Method in Class SMS_EPAlert"
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
ms.assetid: 2637f1c4-037b-4f91-b0d3-ce61e9eeb63bsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Close Method in Class SMS_EPAlert
The `Close` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, postpones the alert.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Close(  
     string Comments,  
     datetime SkipUntil  
);  
```  

#### Parameters  
 `Comments`  
 Data type: `String`  

 Qualifiers: `[in, optional]`  

 Administrator-supplied comments for the postpone action.  

 `SkipUntil`  
 Data type: `DateTime`  

 Qualifiers: `[out, optional]`  

 Do not start the evaluation until the specified time.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Alert Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_alert-server-wmi-class.md)   
 [Alert System WMI Server Classes](../../../../../develop/reference/core/servers/manage/alert-system-server-wmi-classes.md)
