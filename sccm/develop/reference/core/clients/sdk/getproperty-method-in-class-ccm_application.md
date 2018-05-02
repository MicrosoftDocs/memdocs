---
title: "GetProperty Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 564b89ee-b9bb-459d-a8cc-1babb6220757
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetProperty Method in Class CCM_Application
The `GetProperty` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets an application property value.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetProperty   
{  
    [IN]    UInt32 LanguageId  
    [IN]    String PropertyName  
    [OUT]   String PropertyValue  
};  
```  

## Parameters  
 `LanguageId`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Language identifier.    

 `PropertyName`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Property name.    

 `PropertyValue`  
 Data type: `String`  

 Qualifiers: [id("2"), out]  

 Property value.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
