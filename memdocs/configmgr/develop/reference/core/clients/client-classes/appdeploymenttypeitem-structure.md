---
title: AppDeploymentTypeItem Structure
titleSuffix: Configuration Manager
description: Learn about the AppDeploymentTypeItem structure that contains detection results for an individual deployment type.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f5c6cf80-8c02-4a8e-aa33-de91ebef8053
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
