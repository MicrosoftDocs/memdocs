---
description: Learn how to set the code of the source site of the package using SetSourceSite class method in Configuration Manager.
title: SetSourceSite method in class SMS_Package
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# SetSourceSite Method in Class SMS_Package
The `SetSourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the code of the source site for the package.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 SetSourceSite(
      String SourceSite
);
```

#### Parameters
 `SourceSite`
 Data type: `String`

 Qualifiers: [in]

 The site code of the source site for the package.

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
