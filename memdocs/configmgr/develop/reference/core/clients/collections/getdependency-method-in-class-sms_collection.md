---
title: GetDependency method
titleSuffix: Configuration Manager
description: Get the collection relationship info which the input collection depends on.
ms.date: 11/30/2020
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 32efccb1-4a3a-4811-902d-e26dd9c9c7ba
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# GetDependency method in class SMS_Collection

Starting in version 2010, the `GetDependency` WMI class method in Configuration Manager gets the collection relationship info which the input collection depends on.

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax  

```MOF
sint32 GetDependency(
    string Relationship[]
);
```

## Parameters

### `Relationship`

Data type: `String[]` (array)

Qualifiers: [out]

JSON string array of collection dependency relationship.

## Return values

An `SInt32` data type that is `0` to indicate success, or non-zero to indicate failure.

For more information about handling returned errors, see [About Configuration Manager errors](../../../../core/understand/about-configuration-manager-errors.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../../core/reqs/server-development-requirements.md).

## See also

[SMS_Collection server WMI class](sms_collection-server-wmi-class.md)

[GetDependent method](getdependent-method-in-class-sms_collection.md)
