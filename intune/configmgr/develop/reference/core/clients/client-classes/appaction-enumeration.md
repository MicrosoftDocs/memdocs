---
title: AppAction Enumeration
description: Learn how the AppAction enumeration defines action types.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
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
