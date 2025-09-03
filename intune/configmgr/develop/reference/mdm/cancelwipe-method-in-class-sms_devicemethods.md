---
title: CancelWipe Method
titleSuffix: Configuration Manager
description: The CancelWipe Windows Management Instrumentation (WMI) class method cancels a pending wipe request on mobile devices or Exchange ActiveSync devices.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5cd73769-af3f-46c3-93d2-4b0391173b64
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# CancelWipe Method in Class SMS_DeviceMethods
The `CancelWipe` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels a pending wipe request on mobile devices or Exchange ActiveSync devices.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 CancelWipe(
   UInt32 ResourceId
);
```

#### Parameters
 `ResourceId`
 Data type: `UInt32`

 Qualifiers: [in]

 Identifier of the resource for which to cancel the wipe.

## Return Values
 An `SInt32`data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## See Also
 [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)
