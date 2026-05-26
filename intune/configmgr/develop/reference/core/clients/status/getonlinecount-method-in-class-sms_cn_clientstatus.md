---
description: Learn how to get an online count of the selected clients of the target collection using GetOnlineCount class method.
title: GetOnlineCount Method
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetOnlineCount Method in Class SMS_CN_ClientStatus
The `GetOnlineCount` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets an online count of the selected clients of the target collection.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetOnlineCount
{
    [IN]    String TargetCollectionID
    [IN]    Uint32 TargetResourceIDs[]
};
```

## Parameters
 `TargetCollectionID`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Target collection identifier.

 `TargetResourceIDs`
 Data type: `UInt32` Array

 Qualifiers: [id("1"), in]

 Target client resource identifiers.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
