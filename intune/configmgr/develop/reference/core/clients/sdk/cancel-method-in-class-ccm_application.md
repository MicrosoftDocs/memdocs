---
description: Learn how to cancel an application deployment using the Cancel class method in Configuration Manager.
title: Cancel Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6e3884b5-1598-4c54-b22a-da4518dea323
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# Cancel Method in Class CCM_Application
The `Cancel` Windows Management Instrumentation (WMI) class method in Configuration Manager that cancels an application deployment.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
uint32 Cancel
{
    [IN]    String Id
    [IN]    String Revision
    [IN]    Boolean IsMachineTarget
};
```

## Parameters
 `Id`
 Data type: `String`

 Qualifiers: [id("0"), in]

 Application identifier.

 `Revision`
 Data type: `String`

 Qualifiers: [id("1"), in]

 Revision.

 `IsMachineTarget`
 Data type: `Boolean`

 Qualifiers: [id("2"), in]

 `true` if the application targets a device.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
