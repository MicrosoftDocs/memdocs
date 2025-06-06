---
description: Learn how to map a role and its associated object types in Configuration Manager using the SMS_RoleInObjectType class.
title: SMS_RoleInObjectType Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 849fb64d-23d4-4642-b5bc-92168a35b2c1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_RoleInObjectType Server WMI Class
The `SMS_RoleInObjectType` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager that maps a role and its associated object types.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_RoleInObjectType : SMS_BaseClass
{
    UInt32 ObjectTypeID;
    String RoleID;
};
```

## Methods
 The `SMS_RoleInObjectType` class doesn't define any methods.

## Properties
 `ObjectTypeID`
 Data type: `UInt32`

 Access type: Read/Write

 Qualifiers: [key]

 Secured object class ID. Possible values are listed below.

| Value | Object type ID |
| ----- | -------------- |
|2|SMS_Package|
|14|SMS_OperatingSystemInstallPackage|
|18|SMS_ImagePackage|
|19|SMS_BootImagePackage|
|21|SMS_DeviceSettingPackage|
|23|SMS_DriverPackage|
|24|SMS_SoftwareUpdatesPackage|
|31|SMS_Application|

 `RoleID`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key]

 The ID of the role.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
