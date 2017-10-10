---
title: "CCM_ApplicationActions Class"
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
ms.assetid: 1e9fe422-4ef6-4c7a-9f17-df26fb4bf5e2searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_ApplicationActions Client WMI Class
The `CCM_ApplicationActions` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application actions.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_ApplicationActions :    
{  
    DateTime NextGlobalRevalTime;  
    DateTime NextRetryTime;  
    DateTime NextServiceWindowTime;  
};  
```  

## Methods  
 The `CCM_ApplicationActions` class does not define any methods.  

## Properties  
 `NextGlobalRevalTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Next global reevaluation time.    

 `NextRetryTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Next retry time    

 `NextServiceWindowTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Next service window time.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
