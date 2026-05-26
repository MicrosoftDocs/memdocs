---
description: Learn how to get the extended data that the current user and its groups have using GetAdminExtendedData.
title: GetAdminExtendedData Method
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# GetAdminExtendedData Method in Class SMS_Admin
The `GetAdminExtendedData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the extended data that the current user and its groups have for a given type.

> [!WARNING]
>  This method is reserved for internal use.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
sint32 GetAdminExtendedData(
    [in] uint32 Type,
    [out] string ExtendedData[]);
};
```

#### Parameters
 `Type`
 Data type: `UInt32`

 Qualifiers: [in]

 The type associated with the user.

 `ExtendedData`
 Data type: `String` Array

 Qualifiers: [out]

 The extended data that the current user and its groups have for a given type.

## Return Values
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_Admin Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_admin-server-wmi-class.md)
