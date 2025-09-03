---
title: UpdateAutoUpgradeConfigs Method
titleSuffix: Configuration Manager
description: The UpdateAutoUpgradeConfigs Windows Management Instrumentation class method, in Configuration Manager, updates configurations for autoupgrade settings.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 4214f7a0-03e3-4e3a-bb31-5b958e45c5d0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# UpdateAutoUpgradeConfigs Method in Class SMS_Site
The `UpdateAutoUpgradeConfigs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates configurations for autoupgrade settings.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 UpdateAutoUpgradeConfigs(
     String ClientVersion,
     Boolean IsProgramEnabled,
     UInt32 AdvertisementDuration,
     UInt32 ValidationInterval,
     UInt32 ValidationFailureInterval,
     Boolean AllowPrestage,
     Boolean AllowFallbackToContentSource,
     UInt32 DownloadOptionsInSlowNetwork,
     Boolean ExcludeServers,
     Boolean OverrideServiceWindow,
     Boolean IgnoreNonPersistableVM
);
```

#### Parameters
 `ClientVersion`
 Data type: `String`

 Qualifiers: [in]

 The version of the client.

 `IsProgramEnabled`
 Data type: `Boolean`

 Qualifiers: [in]

 `true` if the program is enabled.

 `AdvertisementDuration`
 Data type: `UInt32`

 Qualifiers: [in]

 Advertisement duration in days.

 `ValidationInterval`
 Data type: `UInt32`

 Qualifiers: [in]

 Validation interval in hours, if the previous validation is successful.

 `ValidationFailureInterval`
 Data type: `UInt32`

 Qualifiers: [in]

 Validation interval in hours, if the previous validation is failed.

 `AllowPrestage`
 Data type: `Boolean`

 Qualifiers: [in]

 `true` if autoupgrade package distributed to pre-stage distribution point is allowed.

 `AllowFallbackToContentSource`
 Data type: `Boolean`

 Qualifiers: [in]

 `true` if fallback to content source is allowed.

 `DownloadOptionInSlowNetwork`
 Data type: `UInt32`

 Qualifiers: [in]

 Download options in slow network. Possible values are:

|Value|Download option|
|-|-|
|0|Do not download.|
|1|Download from distribution point and run locally.|
|2|Run from distribution point.|

 `ExcludeServers`
 Data type: `Boolean`

 Qualifiers: [in]

 Indicates whether autoupgrade should be skipped on servers.

 `OverrideServiceWindow`
 Data type: `Boolean`

 Qualifiers: [in]

 Indicates whether the upgrade on the client occurs in service window.

 `IgnoreNonPersistableVM`
 Data type: `Boolean`

 Qualifiers: [in]

 Indicates whether autoupgrade should be skipped on non-persistent virtual machines.

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
