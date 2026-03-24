---
title: Start method
description: In Configuration Manager, The Start WMI class method is invoked to start a Microsoft Azure service that represents a cloud distribution point for Configuration Manager.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---

# Start method in class SMS_AzureService

The `Start` WMI class method in Configuration Manager that's invoked to start a Microsoft Azure service that represents a cloud distribution point for Configuration Manager.

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 Start
{
    [IN]    UInt32 AzureServiceID
};
```

## Parameters
 `AzureServiceID`
 Data type: `UInt32`

 Qualifiers: [id("0"), in]

 The service identifier key for the `SMS_AzureService` instance on which the current task will be performed.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
