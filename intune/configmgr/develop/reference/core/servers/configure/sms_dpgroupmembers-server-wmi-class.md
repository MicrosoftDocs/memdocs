---
description: The SMS_DPGroupMembers Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents distribution point group members.
title: SMS_DPGroupMembers Class
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# SMS_DPGroupMembers Server WMI Class
The `SMS_DPGroupMembers` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point group members.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_DPGroupMembers : SMS_BaseClass
{
    String DPNALPath;
    String GroupID;
};
```

## Methods
 The `SMS_DPGroupMembers` class does not define any methods.

## Properties
 `DPNALPath`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 Distribution point NAL path.

 `GroupID`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 Unique identifier of the distribution point group.

## Requirements

### Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
