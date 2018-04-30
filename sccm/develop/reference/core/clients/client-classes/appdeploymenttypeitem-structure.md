---
title: "AppDeploymentTypeItem Structure"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f5c6cf80-8c02-4a8e-aa33-de91ebef8053
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
