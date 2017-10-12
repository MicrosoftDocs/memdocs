---
title: "ICCMEvent::Submit Method"
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
ms.assetid: cc15a6d7-3cd4-4718-a9ab-bf1654d05e8dsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ICCMEvent::Submit Method
In Configuration Manager, the `ICcmEvent::Submit` method submits an event to Windows Management Instrumentation (WMI).  

## Syntax  

```  
[C++]  
HRESULT ICcmEvent::Submit();  
```  

#### Parameters  
 None.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded.  

## Requirements  
 Smscore.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
