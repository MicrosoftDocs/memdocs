---
title: AddSource Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
description: In Configuration Manager, the AddSource Windows Management Instrumentation class method adds a source for the relationship between the user and the device.
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: ca7131e5-528e-4a93-9cb6-b02229252231
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# AddSource Method in Class SMS_UserMachineRelationship
The `AddSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds a source for the relationship between the user and the device.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 AddSource(
     uint32 SourceId
);
```

#### Parameters
 `SourceId`
 Data type: `UInt32`

 Qualifiers: `[in]`

 Source object identifier for dependency.

## Return Values
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)
