---
title: GetClientVersion Method in
titleSuffix: Configuration Manager
description: The GetClientVersion Windows Management Instrumentation (WMI) class method returns the client version.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7a5f103c-2967-45fa-9228-d73e1a6391ee
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# GetClientVersion Method in Class CCM_SoftwareCatalogUtilities
The `GetClientVersion` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that returns the client version.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 GetClientVersion
{
    [OUT]   String ClientVersion
};
```

## Parameters
 `ClientVersion`
 Data type: `String`

 Qualifiers: [id("0"), out]

 Version number of the installed client software.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
