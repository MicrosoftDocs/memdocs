---
title: "GetClientInfo Method"
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
ms.assetid: 1049b6e8-d80d-4678-be17-e622b3a325eesearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetClientInfo Method in Class SMS_Site
The `GetClientInfo` Windows Management Instrumentation (WMI) class method, in Configuration Manager,  gets information about a client.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetClientInfo(  
     String PublishedClientVersion,  
     String AvailableClientVersion  
);  
```  

#### Parameters  
 `PublishedClientVersion`  
 Data type: `String`  

 Qualifiers: [out]  

 The version of the client that has been published.  

 `AvailableClientVersion`  
 Data type: `String`  

 Qualifiers: [out]  

 The version of the client that is available at the site server.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
