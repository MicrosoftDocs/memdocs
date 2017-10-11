---
title: "CIDetectInfo Structure"
titleSuffix: "Configuration Manager"
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
ms.assetid: c719e7cf-481b-44ee-92db-60de1b4e5581searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CIDetectInfo Structure
In System Center Configuration Manager, the `CIDetectInfo` structure contains identity information for baseline configuration item detection.  

## Syntax  

```  
struct CIDetectInfo  
{  
      LPWSTR szCIID;  
      LPWSTR szVersion;  
};  
```  

## Members  
 szCIID  
 ID of the configuration item.  

 szVersion  
 Version of the configuration item.  

## See Also  
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)
