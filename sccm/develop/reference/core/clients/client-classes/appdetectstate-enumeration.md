---
title: "AppDetectState Enumeration"
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
ms.assetid: 68bdc4d6-31f9-4b50-964a-9fe82a32f548searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# AppDetectState Enumeration
In Configuration Manager, the `AppDetectState` enumeration defines application installation states. This enumeration is used by the [IAppManagementHandler Interface](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler-interface.md).  

## Syntax  

```  
typedef enum tagAppDetectState  
{  
    appDetectNotFound = 0,   
    appDetectInstalled,   
    appDetectFailed  
}AppDetectState;  

```  

## Elements  
 `appDetectNotFound`  
 The application was not found.  

 `appDetectInstalled`  
 The application is installed.  

 `appDetectFailed`  
 Application detection failed.  

## Remarks  
 This enumeration is used by the [IAppManagementHandler Interface](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler-interface.md).  

## See Also  
 [Application Management Client Interfaces](../../../../../develop/reference/core/clients/client-classes/application-management-client-interfaces.md)   
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
