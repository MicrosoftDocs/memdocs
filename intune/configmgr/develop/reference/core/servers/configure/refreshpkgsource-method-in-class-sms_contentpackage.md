---
title: RefreshPkgSource method in class SMS_ContentPackage
description: The RefreshPkgSource Windows Management Instrumentation (WMI) class method causes a refresh of the package source.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# RefreshPkgSource Method in Class SMS_ContentPackage
The `RefreshPkgSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, causes a refresh of the package source.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 RefreshPkgSource();
```

#### Parameters
 None.

## Remarks
 This method is used when the package properties haven't changed.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)
