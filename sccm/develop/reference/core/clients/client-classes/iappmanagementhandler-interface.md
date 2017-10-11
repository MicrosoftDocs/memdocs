---
title: "IAppManagementHandler Interface"
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
ms.assetid: 674e4aa0-f1bf-45f5-b369-4c0592a93b57searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IAppManagementHandler Interface
The `IAppManagementHandler` interface, in Configuration Manager defines functions to interact with the handler.  

 The interface inherits from `IUnknown`.  

## In This Section  
 The following table lists the methods in the `IAppManagementHandler` interface.  

|Term|Definition|  
|----------|----------------|  
|[IAppManagementHandler::CheckReconnectData Method](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--checkreconnectdata-method.md)|The `IAppManagementHandler::CheckReconnectData` method, in Configuration Manager, checks whether the reconnection data is valid.|  
|[IAppManagementHandler::CompleteEnforcement Method](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--completeenforcement-method.md)|The `IAppManagementHandler::CompleteEnforcement` method, in Configuration Manager, completes the installation of a specific application. This method will be called only when the handler returned valid reconnection data in the EnforceApp call.|  
|[IAppManagementHandler::DiscoverApp Method](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--discoverapp-method.md)|The `IAppManagementHandler::DiscoverApp` method, in Configuration Manager, runs a synchronous discovery operation for the provided synclet.|  
|[IAppManagementHandler::EnforceApp Method](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--enforceapp-method.md)|The `IAppManagementHandler::EnforceApp` method, in Configuration Manager, starts the installation of a specific application.|  
|[IAppManagementHandler::EnumerateApps Method](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--enumerateapps-method.md)|The `IAppManagementHandler::EnumerateApps` method, in Configuration Manager, runs a synchronous discovery operation for the provided synclet.|  
|[IAppManagementHandler::GetPendingComponentList Function](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler--getpendingcomponentlist-method.md)|The `IAppManagementHandler::GetPendingComponentList` method, in Configuration Manager, gets the pending component list for a specified deployment type.|  

## Remarks  
 To obtain this interface, the application calls the `IAppManagementHandler` interface.  

## UUID  
 The UUID for `IAppManagementHandler` is B206D835-6BD3-4e70-952E-FBA99AEBC5CE.  

## See Also  
 [Application Management Client Interfaces](../../../../../develop/reference/core/clients/client-classes/application-management-client-interfaces.md)   
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
