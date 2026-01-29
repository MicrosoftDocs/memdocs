---
title: VerifyPackage Method
description: A class method that verifies the integrity of the files in a package by calculating the hash of each file.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# VerifyPackage Method in Class SMS_DistributionPoint
The `VerifyPackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, verifies the integrity of all the files in the package by calculating the hash of each file.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 VerifyPackage(
     string PackageId,
     string NALPath
);
```

#### Parameters
 `PackageId`
 Data type: `String`

 Qualifiers: `[in]`

 ID for an existing package.

 `NALPath`
 Data type: `String`

 Qualifiers: `[in]`

 Network abstraction layer (NAL) path to the distribution point server.

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
