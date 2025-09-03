---
title: CancelRetire Method
titleSuffix: Configuration Manager
description: The CancelRetire WMI class method cancels the retirement of this device from Configuration Manager.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5133539e-f4a6-48fa-a18a-f699ae587e76
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# CancelRetire Method in Class SMS_DeviceMethods
The `CancelRetire` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels the retirement of this device from Configuration Manager (the device will remain managed by Configuration Manager).

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 CancelRetire(
   UInt32 ResourceId
);
```

#### Parameters
 `ResourceId`
 Data type: `UInt32`

 Qualifiers: [in]

 ID of the resource.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## See Also
 [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)
