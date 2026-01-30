---
description: Learn how the SMS_FailedImageUpdateView Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager that represents failed software update information in offline servicing image.
title: SMS_FailedImageUpdateView Class
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# SMS_FailedImageUpdateView Server WMI Class
The `SMS_FailedImageUpdateView` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager that represents failed software update information in offline servicing image.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_FailedImageUpdateView : SMS_BaseClass
{
    SInt32 FailedImageCount;
    String Title;
    SInt32 UpdateID;
};
```

## Methods
 The `SMS_FailedImageUpdateView` class doesn't define any methods.

## Properties
 `FailedImageCount`
 Data type: `SInt32`

 Access type: Read/Write

 Qualifiers: none

 Offline image count that failed to install this update.

 `Title`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 Software update display name.

 `UpdateID`
 Data type: `SInt32`

 Access type: Read/Write

 Qualifiers: [key]

 Software update local unique ID.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
