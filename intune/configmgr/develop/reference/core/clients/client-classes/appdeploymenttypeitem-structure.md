---
title: AppDeploymentTypeItem Structure
description: Learn about the AppDeploymentTypeItem structure that contains detection results for an individual deployment type.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
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
