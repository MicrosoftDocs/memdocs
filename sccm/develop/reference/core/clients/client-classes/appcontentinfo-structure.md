---
title: "AppContentInfo Structure"
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
ms.assetid: eae48844-c1fe-4dd1-9c76-21d7f53217b6searchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
