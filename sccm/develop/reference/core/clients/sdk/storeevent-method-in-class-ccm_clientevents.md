---
title: "StoreEvent Method"
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
ms.assetid: 4c39ecd5-8b90-4034-badc-88529defb3f8searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# StoreEvent Method in Class CCM_ClientEvents
The `StoreEvent` Windows Management Instrumentation (WMI) class method generates store events.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  

 uint32 StoreEvent  
{  
     UInt32 DurationMS,  
     String ComponentName,  
     String EventName,  
     String SessionId  
 };  

```  

## Parameters  
 `DurationMS`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The duration of the event in milliseconds.  

 `ComponentName`  
 Data type: `String`  

 Qualifiers: [in]  

 The name of the component.  

 `EventName`  
 Data type: `String`  

 Qualifiers: [in]  

 The name of the event.  

 `SessionId`  
 Data type: `String`  

 Qualifiers: [in]  

 The ID of the session.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [CCM_ClientEvents Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_clientevents-client-wmi-class.md)   
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
