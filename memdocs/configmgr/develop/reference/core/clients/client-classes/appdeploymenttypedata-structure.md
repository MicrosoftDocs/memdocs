---
title: AppDeploymentTypeData Structure
titleSuffix: Configuration Manager
description: The AppDeploymentTypeData structure contains detection results for a set of deployment types.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7adb722c-0a96-4580-bf2b-4f381e9b5a95
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AppDeploymentTypeData Structure
In Configuration Manager, the `AppDeploymentTypeData` structure contains detection results for a set of deployment types.  

## Syntax  

```  
typedef struct tagAppDeploymentTypeData  
{  
    DWORD cbSize;  
    DWORD dwCount;  
    PAppDeploymentTypeItem pData;  
}AppDeploymentTypeData;  
```  

## Members  
 `cbSize`  
 The size of this structure to indicate version.  

 `dwCount`  
 The number of discovered items.  

 `PAppDeploymentTypeItem`  
 An array of discovered items.  

## See Also  
 [Application Management Client Interfaces](../../../../../develop/reference/core/clients/client-classes/application-management-client-interfaces.md)   
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
