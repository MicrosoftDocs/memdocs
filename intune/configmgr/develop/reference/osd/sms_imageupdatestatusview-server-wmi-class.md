---
title: SMS_ImageUpdateStatusView Class
titleSuffix: Configuration Manager
description: The SMS_ImageUpdateStatusView WMI class represents software update information that is used by offline servicing image.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5a94bf9c-d78e-4a52-883a-de2d9532ada6
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_ImageUpdateStatusView Server WMI Class
The `SMS_ImageUpdateStatusView` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents software update information that is used by offline servicing image.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_ImageUpdateStatusView : SMS_BaseClass
{
    SInt32 ErrorCode;
    SInt32 ImageIndex;
    String ImagePackageID;
    String PackageDescription;
    String PackageName;
    SInt32 UpdateID;
};
```

## Methods
 The `SMS_ImageUpdateStatusView` class does not define any methods.

## Properties
 `ErrorCode`
 Data type: `SInt32`

 Access type: Read/Write

 Qualifiers: none

 Error code for software update installation.

 `ImageIndex`
 Data type: `SInt32`

 Access type: Read/Write

 Qualifiers: [key]

 Index for offline servicing image.

 `ImagePackageID`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 ID for offline servicing image.

 `PackageDescription`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 Description for offline servicing image.

 `PackageName`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 Name for offline servicing image.

 `UpdateID`
 Data type: `SInt32`

 Access type: Read/Write

 Qualifiers: [key]

 ID for software update.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
