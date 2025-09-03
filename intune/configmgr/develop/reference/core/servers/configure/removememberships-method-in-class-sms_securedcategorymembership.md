---
title: RemoveMemberships Method
titleSuffix: Configuration Manager
description: The RemoveMemberships Windows Management Instrumentation (WMI) class method is a batch operation to remove objects from categories.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c4b9f471-d878-49bb-8244-c5004e974e83
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# RemoveMemberships Method in Class SMS_SecuredCategoryMembership
The `RemoveMemberships` Windows Management Instrumentation (WMI) class method, in Configuration Manager, is a batch operation to remove objects from categories.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
SInt32 RemoveMemberships(
    String   ObjectIDs[],
    Uint32   ObjectTypeIDs[],
    String   CategoryIDs[]
);
```

#### Parameters
 `ObjectIDs`
 Data type: `String` Array

 Qualifiers: [in]

 The array of object IDs.

 `ObjectTypeIDs`
 Data type: `UInt32` Array

 Qualifiers: [in]

 The array of corresponding object type ID.

 `CategoryIDs`
 Data type: `String` Array

 Qualifiers: [in]

 The array of corresponding security category IDs which those objects will be removed from.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_SecuredCategoryMembership Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_securedcategorymembership-server-wmi-class.md)
