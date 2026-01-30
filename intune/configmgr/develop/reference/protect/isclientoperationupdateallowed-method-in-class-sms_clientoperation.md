---
title: IsClientOperationUpdateAllowed Method
description: The IsClientOperationUpdateAllowed Windows Management Instrumentation (WMI) class method, in Configuration Manager, that checks whether a user has permission to update an operation. The following syntax is simplified from Managed Object Format (MOF) code and defines the method.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# IsClientOperationUpdateAllowed Method in Class SMS_ClientOperation
The `IsClientOperationUpdateAllowed` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that checks whether a user has permission to update an operation.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 IsClientOperationUpdateAllowed
{
    [IN]    UInt32 OperationID
};
```

## Parameters
 `OperationID`
 Data type: `UInt32`

 Qualifiers: [id("0"), in]

 OperationID.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
