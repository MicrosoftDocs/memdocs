---
title: SMS_BoundaryGroupMembers Class
description: Learn how the SMS_BoundaryGroupMembers Windows Management Instrumentation (WMI) class is an SMS Provider server class that represents boundary group members.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3a193a6a-69ac-431f-a035-635d9aea81cc
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_BoundaryGroupMembers Server WMI Class
The `SMS_BoundaryGroupMembers` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents boundary group members.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_BoundaryGroupMembers : SMS_BaseClass
{
    UInt32 BoundaryID;
    UInt32 GroupID;
};
```

## Methods
 The `SMS_BoundaryGroupMembers` class does not define any methods.

## Properties
 `BoundaryID`
 Data type: `UInt32`

 Access type: Read/Write

 Qualifiers: [key]

 Unique identifier of the boundary.

 `GroupID`
 Data type: `UInt32`

 Access type: Read/Write

 Qualifiers: [key]

 Unique identifier for the boundary group.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
