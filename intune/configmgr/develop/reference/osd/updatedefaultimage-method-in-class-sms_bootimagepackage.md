---
title: UpdateDefaultImage Method
titleSuffix: Configuration Manager
description: Creates a copy of the .wim image pointed to by the ImagePath property. This method expects an SMS_BootImagePackage instance with the ImagePath property being a valid .wim image.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 77b6c163-3cdb-4188-9dd4-e744ad5370c4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# UpdateDefaultImage Method in Class SMS_BootImagePackage
The `UpdateDefaultImage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, creates a copy of the .wim image pointed to by the `ImagePath` property and injects it with operating system deployment files for boot image deployment.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 UpdateDefaultImage();
```

#### Parameters
 None.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Remarks
 This method expects an `SMS_BootImagePackage` instance with the `ImagePath` property being a valid .wim image.

 Your application calls this method only when Configuration Manager is upgrading from an operating system release candidate to an RTM version.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)
