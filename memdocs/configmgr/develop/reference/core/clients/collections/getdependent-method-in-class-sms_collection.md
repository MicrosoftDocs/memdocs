---
title: GetDependent method
titleSuffix: Configuration Manager
description: Get the collection relationship info which depends on the input collection.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# GetDependent method in class SMS_Collection

Starting in version 2010, the `GetDependent` WMI class method in Configuration Manager gets the collection relationship info which depends on the input collection.

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax  

```MOF
sint32 GetDependent(
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

[GetDependency method](getdependency-method-in-class-sms_collection.md)
