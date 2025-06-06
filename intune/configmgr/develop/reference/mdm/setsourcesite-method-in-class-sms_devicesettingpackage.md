---
title: SetSourceSite method in class SMS_DeviceSettingPackage
titleSuffix: Configuration Manager
description: The SetSourceSite WMI class method sets the code of the source site for the device setting package.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 74fbfebb-62da-42c8-a67b-45192a660cf4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SetSourceSite Method in Class SMS_DeviceSettingPackage
The `SetSourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the code of the source site for the device setting package.

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

 The code of the source site for the device setting package.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## See Also
 [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md)
 [RefreshPkgSource Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/refreshpkgsource-method-in-class-sms_devicesettingpackage.md)
