---
description: Learn how to update the enabled/disabled state of a feature using UpdateFeatureState WMI class method.
title: UpdateFeatureState Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 04077212-ba47-4e6b-8e98-80f99051c1d8
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# UpdateFeatureState Method in Class SMS_Site
The `UpdateFeatureState` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the enabled/disabled state of a feature.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 UpdateFeatureState (
     String SiteCode,
     UInt32 FeatureID,
     Boolean IsEnabled
);
```

#### Parameters
 `SiteCode`
 Data type: `String`

 Qualifiers: [in]

 Site code of site to check. NULL indicates the current site.

 `FeatureID`
 Data type: `UInt32`

 Qualifiers: [in]

 Feature identifier. Possible values are:

|Value|Feature identifier|
|-|-|
|1|SleepServer|

 `IsEnabled`
 Data type: `Boolean`

 Qualifiers: [in]

 `true` if the feature is enabled.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
