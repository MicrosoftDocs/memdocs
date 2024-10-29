---
description: Learn how to define application installation states in Configuration Manager using AppDetectState enumeration.
title: AppDetectState Enumeration
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 68bdc4d6-31f9-4b50-964a-9fe82a32f548
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
