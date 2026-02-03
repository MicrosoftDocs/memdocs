---
description: Article outlining the use of the GetSuppressComputerActivityInPresentationMode in Configuration Manager.
title: GetSuppressComputerActivityInPresentationMode Method
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetSuppressComputerActivityInPresentationMode Method in Class CCM_ClientUXSettings
The `GetSuppressComputerActivityInPresentationMode` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets the value for `SuppressComputerActivityInPresentationMode`

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetSuppressComputerActivityInPresentationMode
{
    [OUT]   Boolean SuppressComputerActivityInPresentationMode
};
```

## Parameters
 `SuppressComputerActivityInPresentationMode`
 Data type: `Boolean`

 Qualifiers: [id("0"), out]

 `true` to suppress computer activity in presentation mode.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
