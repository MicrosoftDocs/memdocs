---
title: SMS_DriverContainer Class
description: In Configuration Manager, the SMS_DriverContainer Windows Management Instrumentation class is an SMS Provider server class that represents boot image or driver package information that refers to the specified driver.
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# SMS_DriverContainer Server WMI Class
The `SMS_DriverContainer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents boot image or driver package information that refers to the specified driver.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_DriverContainer : SMS_BaseClass
{
    UInt32 CI_ID;
    String Name;
    String PackageID;
    UInt32 PackageType;
};
```

## Methods
 The `SMS_DriverContainer` class does not define any methods.

## Properties
 `CI_ID`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [key, not_null, read]

 The unique ID of the driver configuration item.

 `Name`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 Driver package or boot image name.

 `PackageID`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [key, not_null, read]

 Driver package or boot image ID.

 `PackageType`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [enumeration, read]

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
