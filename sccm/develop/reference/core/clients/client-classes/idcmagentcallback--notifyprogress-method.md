---
title: "IDCMAgentCallback::NotifyProgress"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 99e6837e-49af-4b57-8b79-be8e2c18cbac
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# IDCMAgentCallback::NotifyProgress Method
The `IDCMAgentCallback::NotifyProgress` method, in Configuration Manager, notifies the caller of progress made on a Desired Configuration Management Agent job.  

## Syntax  

```  
[IDL]  
HRESULT NotifyProgress(  
     IDCMAgentJob* pJob,  
     MessageId msgId  
);  
```  

#### Parameters  
 `pJob`  
 Data type: `IDCMAgentJob`  

 Qualifiers: [in]  

 Pointer to the `IDCMAgentJob` object representing the configuration items and their progress.  

 `msgId`  
 Data type: `MessageId`  

 Qualifiers: [in]  

 Nothing is returned for this parameter.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
