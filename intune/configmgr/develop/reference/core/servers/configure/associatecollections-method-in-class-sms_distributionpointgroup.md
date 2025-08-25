---
title: AssociateCollections Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the AssociateCollections WMI class method associates a set of collections to this distribution point group.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cffda6d7-5c0c-481a-ba0d-f3900cbfbb5a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# AssociateCollections Method in Class SMS_DistributionPointGroup
The `AssociateCollections` Windows Management Instrumentation (WMI) class method, in Configuration Manager,  associates a set of collections to this distribution point group.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 AssociateCollections(
     string CollectionID[]
);
```

#### Parameters
 `CollectionID`
 Data type: `String` Array

 Qualifiers: `[in]`

 The ID that refers to the collection.

## Return Values
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)
