---
title: RaiseWarningStatusMsg Method
description: Learn how to use the RaiseWarningStatusMsg method in Configuration Manager to create a warning status message.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 979ac4c3-03b9-41b2-9a3d-371ccbe0695e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# RaiseWarningStatusMsg Method in Class SMS_StatusMessage
The `RaiseWarningStatusMsg` Windows Management Instrumentation (WMI) class method, in Configuration Manager, creates a warning status message.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.

## Syntax

```
UInt32 RaiseWarningStatusMsg(
   String MessageText,
   UInt32 MessageType,
   UInt32 Win32Error,
   UInt32 ProcessID,
   UInt32 ThreadID,
   DateTime Time,
   UInt32 AttrIDs[],
   String AttrValues[],
   String TopLevelSiteCode
);
```

#### Parameters
 `MessageText`
 Data type: `String`

 Qualifiers: [in]

 Text to use in the message.

 `MessageType`
 Data type: `UInt32`

 Qualifiers: [in]

 The message type. Possible values are defined by the `MessageType` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `Win32Error`
 Data type: `UInt32`

 Qualifiers: [in, optional]

 Win32 error code associated with the status message.

 `ProcessID`
 Data type: `UInt32`

 Qualifiers: [in, optional]

 ID of the process that created the message. The default value is 0.

 `ThreadID`
 Data type: `UInt32`

 Qualifiers: [in, optional]

 ID of the thread that created the message. The default value is 0.

 `Time`
 Data type: `DateTime`

 Qualifiers: [in, optional]

 Date and time, in Universal Coordinated Time (UTC), when the status message was created. The default value indicates current time.

 `AttrIDs`
 Data type: `UInt32` Array

 Qualifiers: [in, optional]

 IDs of message attributes.

 `AttrValues`
 Data type: `String` Array

 Qualifiers: [in, optional]

 Values of message attributes.

 `TopLevelSiteCode`
 Data type: `String`

 Qualifiers: [in, optional]

 This property is deprecated.

## Return Values
 A `UInt32` data type.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
