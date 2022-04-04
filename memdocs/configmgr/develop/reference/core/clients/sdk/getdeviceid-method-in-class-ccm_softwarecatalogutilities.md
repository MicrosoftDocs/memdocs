---
description: Learn how to use the GetDeviceId method to return the device (client) identifier.
title: "GetDeviceId Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6c185a47-b593-4a6e-8f59-205e10c2a314
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetDeviceId Method in Class CCM_SoftwareCatalogUtilities
The `GetDeviceId` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that returns the device (client) identifier.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetDeviceId   
{  
    [OUT]   String ClientId  
    [OUT]   String SignedClientId  
};  
```  

## Parameters  
 `ClientId`  
 Data type: `String`  

 Qualifiers: [id("0"), out]  

 Client identifier.    

 `SignedClientId`  
 Data type: `String`  

 Qualifiers: [id("1"), out]  

 Signed client identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
