---
title: "GetOnlineCount Method"
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
ms.assetid: aac8dcfa-8d65-46ff-a86d-9b62a2a16aefsearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetOnlineCount Method in Class SMS_CN_ClientStatus
The `GetOnlineCount` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets an online count of the selected clients of the target collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetOnlineCount  
{  
    [IN]    String TargetCollectionID  
    [IN]    Uint32 TargetResourceIDs[]  
};  
```  

## Parameters  
 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Target collection identifier.  

 `TargetResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [id("1"), in]  

 Target client resource identifiers.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
