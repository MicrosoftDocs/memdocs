---
title: ReleaseAllLocks Method
description: Learn how to use the ReleaseAllLocks method in Configuration Manager to release all locks for a session.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 0ae7a50a-1e8e-4d67-8814-7b0ba0787ca8
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# ReleaseAllLocks Method in Class SMS_ObjectLock
The `ReleaseAllLocks` Windows Management Instrumentation (WMI) class method, in Configuration Manager, releases all locks for a session.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 ReleaseAllLocks();
```

#### Parameters
 None.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_ObjectLock Server WMI Class](../../../develop/reference/misc/sms_objectlock-server-wmi-class.md)
