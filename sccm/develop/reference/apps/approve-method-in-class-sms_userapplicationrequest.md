---
title: "Approve Method"
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
ms.assetid: f1517eea-0a50-40b3-b83a-a20120fd09afsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Approve Method in Class SMS_UserApplicationRequest
The `Approve` Windows Management Instrumentation (WMI) class method, in Configuration Manager, approves user application requests.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Approve(  
     string Comments  
);  
```  

#### Parameters  
 `Comments`  
 Data type: `String` Array  

 Qualifiers: [in, SizeLimit(“2000��?)]  

 Comments regarding the approval of the application request.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserApplicationRequest Server WMI Class](../../../develop/reference/apps/sms_userapplicationrequest-server-wmi-class.md)
