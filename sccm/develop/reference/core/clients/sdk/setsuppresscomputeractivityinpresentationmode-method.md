---
title: "SetSuppressComputerActivityInPresentationMode Method"
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
ms.assetid: d7bf33f9-10e3-4257-938a-fcebaa5c5bd4searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SetSuppressComputerActivityInPresentationMode Method in Class CCM_ClientUXSettings
The `SetSuppressComputerActivityInPresentationMode` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that that sets the value for `SuppressComputerActivityInPresentationMode`.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 SetSuppressComputerActivityInPresentationMode   
{  
    [IN]    Boolean SuppressComputerActivityInPresentationMode  
};  
```  

## Parameters  
 `SuppressComputerActivityInPresentationMode`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), in]  

 `true` to suppress computer activity in presentation mode.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
