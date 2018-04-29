---
title: "AppAction Enumeration"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 859ba1cf-2cc7-499a-ac79-6d4a1095d97f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# AppAction Enumeration
In Configuration Manager, the `AppAction` enumeration defines action types. This enumeration is used by the [IAppManagmentTypes Interface](../../../../../develop/reference/core/clients/client-classes/iappmanagementtypes-interface.md).  

## Syntax  

```  
typedef enum AppAction  
{  
    appDiscovery = 0,   
    appInstall = 1,   
    appUninstall = 2  
}AppAction;  
```  

## Elements  
 `appDiscovery`  
 The action type is discovery.  

 `appInstall`  
 The action type is install.  

 `appUninstall`  
 The action type is uninstall.  

## See Also  
 [IAppManagementTypes Interface](../../../../../develop/reference/core/clients/client-classes/iappmanagementtypes-interface.md)   
 [Application Management Client Interfaces](../../../../../develop/reference/core/clients/client-classes/application-management-client-interfaces.md)   
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
