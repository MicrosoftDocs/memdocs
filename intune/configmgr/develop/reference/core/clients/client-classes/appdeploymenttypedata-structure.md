---
title: AppDeploymentTypeData Structure
description: The AppDeploymentTypeData structure contains detection results for a set of deployment types.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
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
