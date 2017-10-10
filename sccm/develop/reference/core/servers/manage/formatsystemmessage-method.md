---
title: "FormatSystemMessage Method"
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
ms.assetid: 2aaf8fa4-9ad5-4497-af59-7106631969b7searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# FormatSystemMessage Method
The `FormatSystemMessage` method, in Configuration Manager, formats a system error message by using the error code and optional insertion strings.  

## Syntax  

```  
[VBScript]  
SMSFormatMessageCtl.FormatSystemMessage  
```  

#### Parameters  
 `MessageID`  
 Data type: `int`  

 Error message ID.  

 `InsertionStrings`  
 Data type: `object`  

 Optional list of insertion strings.  

## Return Value  
 A string.  

## Requirements  
 FormatMessageCtl.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMSFormatMessageCtl Class](../../../../../develop/reference/core/servers/manage/smsformatmessagectl-class.md)
