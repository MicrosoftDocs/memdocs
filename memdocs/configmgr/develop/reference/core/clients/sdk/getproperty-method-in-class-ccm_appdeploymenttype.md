---
description: Learn how to retrieve an application deployment type property using GetProperty class in Configuration Manager. 
title: GetProperty method in class CCM_AppDeploymentType
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3002c0dd-4713-42c6-bda0-f7cc7d8d1b2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetProperty Method in Class CCM_AppDeploymentType
The `GetProperty` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that retrieves an application deployment type property.   

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
