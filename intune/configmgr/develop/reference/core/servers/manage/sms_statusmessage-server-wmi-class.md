---
title: SMS_StatusMessage Class
titleSuffix: Configuration Manager
description: The SMS_StatusMessage WMI class is an SMS Provider server class, in Configuration Manager, that represents individual status messages generated by Configuration Manager.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 424f4066-e8cc-428b-bd1d-48aa45dcbdfa
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_StatusMessage Server WMI Class
The `SMS_StatusMessage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents individual status messages generated by Configuration Manager to provide information about a variety of events, including process completion, errors, conditions, and user actions.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_StatusMessage : SMS_BaseClass
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
 The following table lists the methods in `SMS_StatusMessage`.

|Method|Description|
|------------|-----------------|
|[DeleteByID Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/deletebyid-method-in-class-sms_statusmessage.md)|Deletes a group of up to 256 status messages.|
|[DeleteByQuery Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/deletebyquery-method-in-class-sms_statusmessage.md)|Deletes a group of status messages specified by a WMI query language SELECT statement.|
|[RaiseErrorStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiseerrorstatusmsg-method-in-class-sms_statusmessage.md)|Creates an error status message.|
|[RaiseInformationalStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiseinformationalstatusmsg-method-in-class-sms_statusmessage.md)|Creates an informational status message.|
|[RaiseRawStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiserawstatusmsg-method-in-class-sms_statusmessage.md)|Creates a status message from an external message DLL.|
|[RaiseWarningStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raisewarningstatusmsg-method-in-class-sms_statusmessage.md)|Creates a warning status message.|

## Properties
 `Component`
 Data type: `String`

 Access type: Read

 Qualifiers: None

 Name of the component that created the message. For user-defined messages, this name comes from the `ApplicationName` context qualifier that you must set before calling a raise status message method.

 `MachineName`
 Data type: `String`

 Access type: Read

 Qualifiers: None

 Name of the computer that created the message. For user-defined messages, this name comes from the `MachineName` context qualifier that you must set before calling a raise status message method.

 `MessageID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: [Range("0-65535")]

 Unique ID of message text in a message DLL. This property is set to the associated value when your application calls a method listed in the following table.

| Value | Message ID |
| ----- | ---------- |
|39997|[RaiseInformationalStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiseinformationalstatusmsg-method-in-class-sms_statusmessage.md)|
|39998|[RaiseWarningStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raisewarningstatusmsg-method-in-class-sms_statusmessage.md)|
|39999|[RaiseErrorStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiseerrorstatusmsg-method-in-class-sms_statusmessage.md)|

 `MessageType`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Type of message. Possible values are:

| Value | Message type |
| ----- | ------------ |
|256|Milestone. Use this type at the end of an operation to indicate the operation's success or failure. If the operation was successful, use the Milestone type in an informational message. If the operation failed, use a milestone message type in a warning or error message.|
|512|Detail. Use this type to illustrate the steps in a complex operation. Often, detail messages are meaningful only within the context of the sequence of status messages representing a complex operation.|
|768|Audit. Use this type for informational messages that provides a trail of actions taken by the Configuration Manager administrator. An audit message also depicts an operation that results in objects being added, modified, or deleted. You do not need to create audit messages; the provider automatically generates these messages for you.|
|1024|NTEvent.|

 `ModuleName`
 Data type: `String`

 Access type: Read

 Qualifiers: None

 The DLL that is associated with the status message. This is not the name of the DLL itself, but a display string corresponding to the `ModuleName` property value defined in the [SMS_StatMsgModuleNames Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md) class. You use the `ModuleName` value to get the DLL name.

 `PerClient`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Value indicating whether the status message was generated by a client component. Possible values are listed below. Messages generated on a per-client basis tend to be quite numerous. Thus, this property provides an easy way to filter them out.

| Value | Message generated per-client |
| ----- | ---------------------------- |
|0|`false`|
|2|`true`|

 `ProcessID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 ID of the process that created the message.

 `RecordID`
 Data type: `SInt64`

 Access type: Read

 Qualifiers: [key]

 Unique ID of the status message.

 `ReportFunction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Report function. Possible values are:

| Value | Report function |
| ----- | --------------- |
|0|Report|
|16|BeginTransaction|
|32|CommitSuccessfulTransaction|
|48|CommitFailedTransaction|
|64|RollbackTransaction|
|80|ReportEX|

 `Severity`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Severity of status message. Possible values are:

| Value | Severity |
| ----- | -------- |
|0x40000000 (1073741824)|Informational|
|0x80000000 (2147483648)|Warning|
|0xC0000000<br /><br /> (3221225472)|Error|

 `SiteCode`
 Data type: `String`

 Access type: Read

 Qualifiers: [SizeLimit("3")]

 Site code of the site that created the message.

 `SuccessfulTransaction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Value indicating the transaction status. Possible values are:

| Value | Transaction status |
| ----- | ------------------ |
|0|Failed|
|8|Successful|

 `ThreadID`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Identifier of the thread that created the message.

 `Time`
 Data type: `DateTime`

 Access type: Read

 Qualifiers: None

 Date and time, in Universal Coordinated Time (UTC), when the status message was created.

 `TopLevelSiteCode`
 Data type: `String`

 Access type: Read

 Qualifiers: [SizeLimit("3")]

 This property is deprecated.

 `Transaction`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Value indicating whether transactions are enabled. Possible values are:

| Value | Transaction enabled |
| ----- | ------------------- |
|0|False|
|4|True|

 `Win32Error`
 Data type: `UInt32`

 Access type: Read

 Qualifiers: None

 Win32 error code associated with the status message.

## Remarks
 Class qualifiers for this class include:

- Read (read-only)

- Secured

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).

  You can this class to generate user-defined status messages.

> [!NOTE]
>  Use the [SMS_StatMsg Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsg-server-wmi-class.md) for a high-performance version of this class.

## Requirements

### Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

### Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).

## See Also
 [SMS_StatMsg Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsg-server-wmi-class.md)
