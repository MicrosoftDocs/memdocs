---
title: SMS_StatMsg Class
titleSuffix: Configuration Manager
description: The SMS_StatMsg WMI class is a high-performance version of SMS_StatusMessage Server WMI Class.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 45d6f901-e4a9-4ae6-8715-7687c26d89b3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_StatMsg Server WMI Class
The `SMS_StatMsg` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is a high-performance version of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_StatMsg : SMS_BaseClass
{
      String Component;
      String MachineName;
      UInt32 MessageID;
      UInt32 MessageType;
      String ModuleName;
      UInt32 PerClient;
      UInt32 ProcessID;
      SInt64 RecordID;
      UInt32 ReportFunction;
      UInt32 Severity;
      String SiteCode;
      UInt32 SuccessfulTransaction;
      UInt32 ThreadID;
      DateTime Time;
      String TopLevelSiteCode;
      UInt32 Transaction;
      UInt32 Win32Error;
};
```

## Methods
 The `SMS_StatMsg` class does not define any methods. None of the `SMS_StatusMessage` methods are supported.

## Properties
 `Component`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 Name of the component that created the message. For user-defined messages, this name comes from the `ApplicationName` context qualifier that you must set before calling a raise status message method.

 `MachineName`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 Name of the computer that created the message. For user-defined messages, this name comes from the `MachineName` context qualifier that you must set before calling a raise status message method.

 `MessageID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Unique ID of message text in a message DLL. See the `MessageID` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `MessageType`
 Data type: `UInt32`

 Access type: Read

 Qualifiers:

 none

 Type of message. See the `MessageType` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `ModuleName`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 The DLL that is associated with the status message to raise. This is not the name of the DLL itself, but it is a display string corresponding to the `ModuleName` property value defined in the [SMS_StatMsgModuleNames Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md) class. You use the `ModuleName` value to get the DLL name.

 `PerClient`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Value indicating if the status message was generated by a client component. See the `PerClient` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `ProcessID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 ID of the process that created the message.

 `RecordID`
 Data type: `SInt64`

 Access type: Read

 Qualifiers: none

 Unique ID of the status message.

 `ReportFunction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Report function. See the `ReportFunction` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `Severity`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Severity of the status message. See the `Severity` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `SiteCode`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 Site code of the site that created the message.

 `SuccessfulTransaction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Value indicating transaction status. See the `SuccessfulTransaction` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `ThreadID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 ID of the thread that created the message.

 `Time`
 Data type: `DateTime`

 Access type: Read

 Qualifiers: none

 Date and time, in Universal Coordinated Time (UTC), when the status message was created.

 `TopLevelSiteCode`
 Data type: `String`

 Access type: Read

 Qualifiers: none

 This property is deprecated.

 `Transaction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Value indicating whether transactions are enabled. See the `Transaction` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).

 `Win32Error`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: none

 Win32 error code that is associated with the status message.

## Remarks
 Class qualifiers for this class include:

- Read (read-only)

- Secured

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
