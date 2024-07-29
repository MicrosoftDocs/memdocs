---
title: "IDCMAgentCallback::NotifyComplete"
titleSuffix: Configuration Manager
description: The IDCMAgentCallback::NotifyComplete method, in Configuration Manager, notifies the caller that a Desired Configuration Management Agent job has completed.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 58e63e77-47ba-4d62-a032-9b77023e281d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IDCMAgentCallback::NotifyComplete Method
The `IDCMAgentCallback::NotifyComplete` method, in Configuration Manager, notifies the caller that a Desired Configuration Management Agent job has completed.  

## Syntax  

```  
[IDL]  
HRESULT NotifyComplete(  
     IDCMAgentJob* pJob  
);  
```  

#### Parameters  
 `pJob`  
 Data type: `IDCMAgentJob`  

 Qualifiers: [in]  

 Pointer to the `IDCMAgentJob` object representing the configuration items and their progress.  

## Return Values  
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
