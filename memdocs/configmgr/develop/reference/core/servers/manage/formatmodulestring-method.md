---
title: "FormatModuleString Method"
titleSuffix: "Configuration Manager"
description: The FormatModuleString method, in Configuration Manager, loads string resources from the resource DLL. 
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8666e465-c05e-435b-a3f8-f57d12a57701
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# FormatModuleString Method
The `FormatModuleString` method, in Configuration Manager, loads string resources from the resource DLL.  

## Syntax  

```  
[VBScript]  
SMSFormatMessageCtl.FormatModuleString   
```  

#### Parameters  
 `ModuleName`  
 Data type: `string`  

 Name of the module to load. The name can be Srvmsgs.dll, Provmsgs.dll, or Climmsgs.dll.  

 `MessageID`  
 Data type: `int`  

 Message ID " combined by using the bitwise OR operation with the severity.  

 `InsertionStrings`  
 Data type: `object`  

 Optional list of insertion strings.  

## Return Value  
 A string.  

## Remarks  
 `FormatModuleString` loads a string that is specified by `MessageID` from a string resource in the `ModuleName` module and inserts the supplied strings.  

## Requirements  
 FormatMessageCtl.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMSFormatMessageCtl Class](../../../../../develop/reference/core/servers/manage/smsformatmessagectl-class.md)
