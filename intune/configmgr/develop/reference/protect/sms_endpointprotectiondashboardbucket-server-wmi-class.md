---
description: Learn how to use SMS_EndpointProtectionDashboardBucket Windows Management Instrumentation (WMI) class in Configuration Manager.
title: SMS_EndpointProtectionDashboardBucket Class
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---

# SMS_EndpointProtectionDashboardBucket Server WMI Class

The `SMS_EndpointProtectionDashboardBucket` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_EndpointProtectionDashboardBucket : SMS_BaseClass
{
    String Bucket;
    String CollectionID;
    String CollectionName;
};
```

## Methods
 The `SMS_EndpointProtectionDashboardBucket` class does not define any methods.

## Properties
 `Bucket`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 Dashboard bucket summarized.

 `CollectionID`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 Identifier of the collection summarized.

 `CollectionName`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 Name of the collection summarized.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
