---
title: "FormatModuleMessage Method"
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
ms.assetid: a7f16c46-de10-4d93-b67b-409c7e3c2991searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# FormatModuleMessage Method
The `FormatModuleMessage` method, in Configuration Manager, resolves Configuration Manager status messages in Srvmsgs.dll, Provmsgs.dll, and Climmsgs.dll.  

## Syntax  

```  
[VBScript]  
SMSFormatMessageCtl.FormatModuleMessage  
```  

#### Parameters  
 `ModuleName`  
 Data type: `string`  

 Name of the module to load. The name can be Srvmsgs.dll, Provmsgs.dll, or Climmsgs.dll.  

 `MessageID`  
 Data type: `int`  

 Message ID logically ORed with the severity.  

 `InsertionStrings`  
 Data type: `object`  

 Optional insertion strings.  

## Return Values  
 A string.  

## Remarks  
 `FormatModuleMessage` loads a string that is specified by `MessageID` from a message resource in the `ModuleName` module and inserts the supplied strings.  

 If insertion strings are not passed in, the message is returned without them. Note that insertion strings are an optional parameter. When retrieving the messages from the Configuration Manager database, you should OR the severity with the `MessageID` parameter. You should also keep the object alive between calls to `FormatModuleMessage` because the object caches module handles. Doing this saves an extra call to `LoadLibrary`.  

## Requirements  
 FormatMessageCtl.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMSFormatMessageCtl Class](../../../../../develop/reference/core/servers/manage/smsformatmessagectl-class.md)
