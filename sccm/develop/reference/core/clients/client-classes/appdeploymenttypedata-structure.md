---
title: "AppDeploymentTypeData Structure"
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
ms.assetid: 7adb722c-0a96-4580-bf2b-4f381e9b5a95searchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
