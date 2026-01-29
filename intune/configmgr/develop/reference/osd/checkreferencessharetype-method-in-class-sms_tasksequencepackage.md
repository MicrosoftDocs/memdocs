---
title: CheckReferencesShareType Method
description: In Configuration Manager, the CheckReferencesShareType WMI class method checks all referred packages for this task sequence and returns all packages that aren't shared.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# CheckReferencesShareType Method in Class SMS_TaskSequencePackage
The `CheckReferencesShareType` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that checks all referred packages for this task sequence and returns all packages that aren't shared.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 CheckReferencesShareType
{
    [IN]    String PackageID
    [OUT]   Boolean CanRunFromDP
    [OUT]   String PacakgeIds[]
    [OUT]   String PackageNames[]
};
```

## Parameters
 `PackageID`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Task sequence package identifier.

 `CanRunFromDP`
 Data type: `Boolean`

 Qualifiers: [id("1"), out]

 `true` if the package can be run from the distribution point.

 `PacakgeIds`
 Data type: `String Array`

 Qualifiers: [id("2"), out]

 Package identifiers for all referred packages for this task sequence that aren't shared.

> [!NOTE]
>  The incorrect spelling of the variable "PacakgeIds" is hardcoded in WMI.

 `PackageNames`
 Data type: `String Array`

 Qualifiers: [id("3"), out]

 Package names for all referred packages for this task sequence that aren't shared.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
