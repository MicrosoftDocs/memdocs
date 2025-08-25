---
description: Learn how to check the state of an empty driver source folder with CheckSourceFolder class im Configuration Manager.
title: CheckSourceFolder Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6b72a1e3-42c3-4481-ab79-f1199d187a28
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# CheckSourceFolder Method in Class SMS_DriverPackage
The `CheckSourceFolder` Windows Management Instrumentation (WMI) class method in Configuration Manager that checks the state of an empty driver source folder.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 CheckSourceFolder
{
    [IN]    String SourceFolder
    [OUT]   SInt32 Result
};
```

## Parameters
 `SourceFolder`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Source folder.

 `Result`
 Data type: `SInt32`

 Qualifiers: [id("1"), out]

 Results of check. Possible values are:

| Value | Result |
| ----- | ------ |
|0|No error.|
|1|The folder isn't in UNC format.|
|2|Can't read/write to the folder.|
|4|The folder isn't empty.|
|8|The folder is already used by another driver package.|

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
