---
title: RequestRetire Method
titleSuffix: Configuration Manager
description: The RequestRetire Windows Management Instrumentation (WMI) class method requests the retirement of this device from Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cdea7272-1dd8-4881-8aa5-692c57d223a1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# RequestRetire Method in Class SMS_DeviceMethods
The `RequestRetire` Windows Management Instrumentation (WMI) class method, in Configuration Manager, requests the retirement of this device from Configuration Manager (the device will no longer be managed by Configuration Manager).

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 RequestRetire(
   UInt32 ResourceId
);
```

#### Parameters
 `ResourceId`
 Data type: `UInt32`

 Qualifiers: [in]

 Identifier of the resource.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## See Also
 [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)
