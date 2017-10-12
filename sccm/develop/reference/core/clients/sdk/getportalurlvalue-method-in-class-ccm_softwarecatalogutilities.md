---
title: "GetPortalUrlValue Method"
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
ms.assetid: e3cc99be-b85e-48dc-87bc-3d27c92987acsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetPortalUrlValue Method in Class CCM_SoftwareCatalogUtilities
The `GetPortalUrlValue` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that returns the portal url for a client.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetPortalUrlValue   
{  
    [OUT]   String PortalUrl  
};  
```  

## Parameters  
 `PortalUrl`  
 Data type: `String`  

 Qualifiers: [id("0"), out]  

 Portal url.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
