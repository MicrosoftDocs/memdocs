---
title: GetPendingComponentList Method
description: In Configuration Manager, the GetPendingComponentList Windows Management Instrumentation class method that gets the pending component list for an application.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetPendingComponentList Method in Class CCM_Application
The `GetPendingComponentList` Windows Management Instrumentation (WMI) class method in Configuration Manager that gets the pending component list for an application.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetPendingComponentList
{
    [IN]    String AppDeliveryTypeId
    [IN]    UInt32 Revision
    [OUT]   String PendingComponentList
};
```

## Parameters
 `AppDeliveryTypeId`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Application delivery type identifier.

 `Revision`
 Data type: `UInt32`

 Qualifiers: [id("1"), in]

 Revision.

 `PendingComponentList`
 Data type: `String`

 Qualifiers: [id("2"), out]

 Pending component list.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
