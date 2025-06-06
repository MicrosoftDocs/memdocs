---
title: Unlock Method in Class SMS_Package
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that sets the source site to the current site, unlocking the package.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6fc6f46e-757d-420f-b6d5-701745f07601
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# Unlock Method in Class SMS_Package
The `Unlock` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site to the current site, unlocking the package.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 Unlock();
```

#### Parameters
 None.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
