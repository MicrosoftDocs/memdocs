---
description: Article outlining the use of the GetSuppressComputerActivityInPresentationMode in Configuration Manager.
title: GetSuppressComputerActivityInPresentationMode Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2286886d-040d-49e6-9739-d2950606b9e2
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetSuppressComputerActivityInPresentationMode Method in Class CCM_ClientUXSettings
The `GetSuppressComputerActivityInPresentationMode` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets the value for `SuppressComputerActivityInPresentationMode`  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetSuppressComputerActivityInPresentationMode   
{  
    [OUT]   Boolean SuppressComputerActivityInPresentationMode  
};  
```  

## Parameters  
 `SuppressComputerActivityInPresentationMode`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), out]  

 `true` to suppress computer activity in presentation mode.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
