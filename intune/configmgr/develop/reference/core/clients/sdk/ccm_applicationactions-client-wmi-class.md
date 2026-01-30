---
description: Learn how to represent application actions using CCM_ApplicationActions class in Configuration Manager.
title: CCM_ApplicationActions Class
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# CCM_ApplicationActions Client WMI Class
The `CCM_ApplicationActions` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application actions.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class CCM_ApplicationActions :
{
    DateTime NextGlobalRevalTime;
    DateTime NextRetryTime;
    DateTime NextServiceWindowTime;
};
```

## Methods
 The `CCM_ApplicationActions` class does not define any methods.

## Properties
 `NextGlobalRevalTime`
 Data type: `DateTime`

 Access type: Read/Write

 Qualifiers: none

 Next global reevaluation time.

 `NextRetryTime`
 Data type: `DateTime`

 Access type: Read/Write

 Qualifiers: none

 Next retry time

 `NextServiceWindowTime`
 Data type: `DateTime`

 Access type: Read/Write

 Qualifiers: none

 Next service window time.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
