---
description: Learn how to represent a client deployment failure bucket used to get the total number of clients with the same failed state message ID.
title: SMS_ClientDeploymentFailureBucket Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8a5608be-1f8a-4aea-a87c-e2b379c98107
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_ClientDeploymentFailureBucket Server WMI Class
The  `SMS_ClientDeploymentFailureBucket` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment failure bucket that is used to get the total number of clients with the same failed state message ID.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_ClientDeploymentFailureBucket: SMS_BaseClass
{
    UInt32 ClientCount;
    String CollectionID;
    UInt32 LastMessageStateID;
};

```

## Methods
 The  `SMS_ClientDeploymentFailureBucket` class does not define any methods.

## Properties
 `ClientCount`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 The total number of clients with the specified LastMessageStateID.

 `CollectionID`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 The ID of the collection of which the clients are members.

 `LastMessageStateID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: [key]

 The ID of the last client deployment state message.

## Remarks
 Class qualifiers for this class include:

- Dynamic

- Read (read-only)

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
