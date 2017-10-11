---
title: "AppDeploymentTypeItem Structure"
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
ms.assetid: f5c6cf80-8c02-4a8e-aa33-de91ebef8053searchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# AppDeploymentTypeItem Structure
In Configuration Manager, the `AppDeploymentTypeItem` structure contains detection results for an individual deployment type.  

## Syntax  

```  
typedef struct tagAppDeploymentTypeItem  
{  
    LPWSTR szId;  
    DWORD dwRevision;  
    AppDetectState eDetectState;  
    DWORD dwErrorCode;  
}AppDeploymentTypeItem, *PAppDeploymentTypeItem;  
```  

## Members  
 `szId`  
 ID of the deployment item.   

 `dwRevision`  
 Revision.   

 `eDetectState`  
 Detect state.   

 dwErrorCode  
 Error code.   

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
