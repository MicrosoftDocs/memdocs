---
title: SetPowerManagementSettings Method
titleSuffix: Configuration Manager
description: A class method that sets power management settings on a client.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 67b81f44-b468-492c-bd79-f4f396861577
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SetPowerManagementSettings Method in Class CCM_PowerManagementSettings
The `SetPowerManagementSettings` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that sets power management settings on a client.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 SetPowerManagementSettings
{
    [IN]  Boolean IsOptOutFromPowerPlan;
    [OUT] UInt32 ReturnValue;
};
```

## Parameters
 `IsOptOutFromPowerPlan`
 Data type: `Boolean`

 Qualifiers: [id("0"), in]

 `true` to allow users to exclude their device from power management.

 `ReturnValue`
 Data type: `UInt32`

 Qualifiers: [out]

 Return value.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
