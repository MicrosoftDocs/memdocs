---
title: "CCM_NetworkSettings Class"
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
ms.assetid: 89c57d32-bb17-470a-82d5-93415fef6bfcsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_NetworkSettings Client WMI Class
The `CCM_NetworkSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents how clients behave on metered Internet connections.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_NetworkSettings :    
{  
    UInt32 MeteredNetworkUsage;  
};  
```  

## Methods  
 The `CCM_NetworkSettings` class does not define any methods.  

## Properties  
 `MeteredNetworkUsage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client communications on metered Internet connections. Possible values are:   

|||  
|-|-|  
|0|Allow|  
|1|Limit|  
|2|Block|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
