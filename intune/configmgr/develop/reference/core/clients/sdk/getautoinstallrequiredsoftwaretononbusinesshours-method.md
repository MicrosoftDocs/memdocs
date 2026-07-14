---
description: Learn how to use the GetAutoInstallRequiredSoftwaretoNonBusinessHours method to get the value for AutomaticallyInstallSoftware.
title: GetAutoInstallRequiredSoftwaretoNonBusinessHours Method
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetAutoInstallRequiredSoftwaretoNonBusinessHours Method in Class CCM_ClientUXSettings
The `GetAutoInstallRequiredSoftwaretoNonBusinessHours` Windows Management Instrumentation (WMI) class method in Configuration Manager that gets the value for `AutomaticallyInstallSoftware`.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetAutoInstallRequiredSoftwaretoNonBusinessHours
{
    [OUT]   Boolean AutomaticallyInstallSoftware
};
```

## Parameters
 `AutomaticallyInstallSoftware`
 Data type: `Boolean`

 Qualifiers: [id("0"), out]

 `true` if necessary software should be automatically installed during nonbusiness hours.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
