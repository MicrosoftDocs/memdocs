---
description: Learn how to represent the base class for SMS_Alert, SMS_EPAlert, and SMS_SCHALert using SMS_AlertBase class.
title: SMS_AlertBase Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7de42b2c-4e70-4354-9bf0-ed9b829ff525
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# SMS_AlertBase Server WMI Class
The `SMS_AlertBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the base class for `SMS_Alert`, `SMS_EPAlert`, and `SMS_SCHAlert` classes.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class SMS_AlertBase : SMS_BaseClass
{
    UInt32 AlertState;
    String ClosedBy;
    String Comments;
    DateTime DateAlertStateModified;
    DateTime DateCreated;
    DateTime DateFirstActivated;
    DateTime DateLastModified;
    Boolean Deletable;
    Boolean Enabled;
    UInt32 FeatureArea;
    UInt32 FeatureGroup;
    UInt32 ID;
    String InstanceNameParam1;
    String InstanceNameParam2;
    String InstanceNameParam3;
    boolean IsIgnored;
    String LastModifiedBy;
    Boolean MonitoredByScom;
    String Name;
    UInt32 NumberOfSubscription;
    UInt32 ObjectTypeID;
    UInt32 OccurrenceCount;
    String ParameterValues;
    String RootCauseMessage;
    SInt32 RuleState;
    UInt32 Severity;
    DateTime SkipUntil;
    String SourceSiteCode;
    UInt32 TypeID;
    String TypeInstanceID;
};
```

## Methods
 The `SMS_AlertBase` class doesn't define any methods.

## Properties
 `AlertState`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read, valuemap, values]

 Current state of this alert.

| Value | Alert state |
| ----- | ----------- |
|0|Active|
|1|Postponed|
|2|Canceled|
|3|Unknown|
|4|Disabled|
|5|Never Triggered|

 `ClosedBy`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 Person who last closed alert, or 'SYSTEM' if canceled.

 `Comments`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 Administrator-supplied comments for this alert.

 `DateAlertStateModified`
 Data type: `DateTime`

 Access type: Read-only

 Qualifiers: [read]

 Date the alert state was last changed.

 `DateCreated`
 Data type: `DateTime`

 Access type: Read-only

 Qualifiers: [read]

 Date the instance was created.

 `DateFirstActivated`
 Data type: `DateTime`

 Access type: Read-only

 Qualifiers: [read]

 Date the alert was first activated.

 `DateLastModified`
 Data type: `DateTime`

 Access type: Read-only

 Qualifiers: [read]

 Date the alert was last changed.

 `Deletable`
 Data type: `Boolean`

 Access type: Read/Write

 Qualifiers: none

 `true` if this alert can be deleted.

 `Enabled`
 Data type: `Boolean`

 Access type: Read/Write

 Qualifiers: none

 `true` if this alert is enabled. When the alert isn't enabled, the condition isn't evaluated.

 `FeatureArea`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read]

 The related feature area.

 `FeatureGroup`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read, valuemap, values]

 A feature group is a set of one or more feature areas.

| Value | Feature group |
| ----- | ------------- |
|1|Administration|
|2|Resources|
|3|Deployment|
|4|Monitoring|
|5|Reporting|

 `ID`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [key, read]

 Unique identifier for this instance.

 `InstanceNameParam1`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 The 1st parameter of the linked instance name.

 `InstanceNameParam2`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 The 2nd parameter of the linked instance name.

 `InstanceNameParam3`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 The 3rd parameter of the linked instance name.

 `IsIgnored`
 Data type: `Boolean`

 Access type: Read-only

 Qualifiers: [read]

 Whether this alert is ignored by the current user.

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.

 `LastModifiedBy`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 Person who last modified the alert.

 `MonitoredByScom`
 Data type: `Boolean`

 Access type: Read/Write

 Qualifiers: none

 Whether this alert is monitored by Operations Manager.

 `Name`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 The name of the alert.

 `NumberOfSubscription`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read]

 The number of subscriptions to this alert.

 `ObjectTypeID`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read]

 The secured object type identifier.

 `OccurrenceCount`
 Data type: `UInt32`

 Access type: Read-only

 Qualifiers: [read]

 The number of times this alert has been activated.

 `ParameterValues`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 The values of administrator-defined parameters, such as thresholds. These values are stored in XML format.

 `RootCauseMessage`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 The root cause of the alert.

 `RuleState`
 Data type: `SInt32`

 Access type: Read-only

 Qualifiers: [read, valuemap, values]

 State of the underlying condition.

| Value | Rule state |
| ----- | ---------- |
|0|Bad|
|1|Good|
|2|Unknown|

 `Severity`
 Data type: `UInt32`

 Access type: Read/Write

 Qualifiers: [valuemap, values]

 The impact of this alert.

| Value | Severity |
| ----- | -------- |
|1|Error|
|2|Warning|
|3|Informational|

 `SkipUntil`
 Data type: `DateTime`

 Access type: Read/Write

 Qualifiers: none

 Don't start the evaluation until the specified time.

 `SourceSiteCode`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: none

 The site code of the source site. For some non-SLA alerts, NULL means it's a global SLA alert.

 `TypeID`
 Data type: `UInt32`

 Access type: Read/Write

 Qualifiers: [not_null]

 Identifier for this type of alert.

 `TypeInstanceID`
 Data type: `String`

 Access type: Read-only

 Qualifiers: [read]

 User-defined identifier. The combination of `TypeID` and `TypeInstanceID` must be unique.

## Remarks

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
