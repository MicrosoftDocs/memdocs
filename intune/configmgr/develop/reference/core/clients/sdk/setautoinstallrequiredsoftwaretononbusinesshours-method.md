---
title: SetAutoInstallRequiredSoftwaretoNonBusinessHours Method
description: The SetAutoInstallRequiredSoftwaretoNonBusinessHours Windows Management Instrumentation class method, in Configuration Manager, sets the value for AutomaticallyInstallSoftware.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# SetAutoInstallRequiredSoftwaretoNonBusinessHours Method in Class CCM_ClientUXSettings
The `SetAutoInstallRequiredSoftwaretoNonBusinessHours` Windows Management Instrumentation (WMI) class method in Configuration Manager that sets the value for `AutomaticallyInstallSoftware`.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 SetAutoInstallRequiredSoftwaretoNonBusinessHours
{
    [IN]    Boolean AutomaticallyInstallSoftware
};
```

## Parameters
 `AutomaticallyInstallSoftware`
 Data type: `Boolean`

 Qualifiers: [id("0"), in]

 `true` if necessary software should be automatically installed during nonbusiness hours.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
