---
title: AppAction Enumeration
titleSuffix: Configuration Manager
description: Learn how the AppAction enumeration defines action types.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 859ba1cf-2cc7-499a-ac79-6d4a1095d97f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
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
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
