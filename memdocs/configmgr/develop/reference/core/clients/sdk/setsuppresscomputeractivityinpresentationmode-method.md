---
title: "SetSuppressComputerActivityInPresentationMode Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d7bf33f9-10e3-4257-938a-fcebaa5c5bd4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetSuppressComputerActivityInPresentationMode Method in Class CCM_ClientUXSettings
The `SetSuppressComputerActivityInPresentationMode` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that sets the value for `SuppressComputerActivityInPresentationMode`.   

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
