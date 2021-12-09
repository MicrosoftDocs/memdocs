---
title: "AppContentInfo Structure"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: eae48844-c1fe-4dd1-9c76-21d7f53217b6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AppContentInfo Structure
In Configuration Manager, the `AppContentInfo` structure contains information about the application content.  

## Syntax  

```  
struct AppContentInfo  
{  
    LPCWSTR szContentId;  
    LPCWSTR szContentVersion;  
    LPCWSTR szLocalPath;  
};  
```  

## Members  
 `szContentId`  
 The content id.  

 `szContentVersion`  
 The content version.  

 `szLocalPath`  
 The local path.  

## See Also  
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
