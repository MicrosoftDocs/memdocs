---
description: Learn how to use the AddDistributionPoints method in Class SMS_Package to add distribution points for the package.
title: AddDistributionPoints Method in Class SMS_Package
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5574c8a9-6e88-4b8c-bafb-104971833826
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# AddDistributionPoints Method in Class SMS_Package
The `AddDistributionPoints` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds the distribution points for the package.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 AddDistributionPoints(
     String SiteCode[],
     String NALPath[]
);
```

#### Parameters
 `SiteCode`
 Data type: `String` Array

 Qualifiers: [in]

 The code for the site to which to add distribution points.

 `NALPath`
 Data type: `String` Array

 Qualifiers: [in]

 Network abstraction layer (NAL) path to the distribution points.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Remarks
 It is not necessary to refresh the distribution points when using this method.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
