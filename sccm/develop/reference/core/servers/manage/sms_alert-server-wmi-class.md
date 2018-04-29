---
title: "SMS_Alert Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: bbf073bd-7b90-4ada-b962-e3f905a86ccf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Alert Server WMI Class
The `SMS_Alert` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents general alerts, which exclude client status alerts and System Center Endpoint Protection alerts.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Alert : SMS_AlertBase  
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
    Boolean IsIgnored;  
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
 The following table lists the methods in the `SMS_Alert` class.  

|Method|Description|  
|------------|-----------------|  
|[Close Method in Class SMS_Alert](../../../../../develop/reference/core/servers/manage/close-method-in-class-sms_alert.md)|Closes an alert.|  

## Properties  
 `AlertState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 Current state of this alert.  

|||  
|-|-|  
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

 Date AlertState was last changed.  

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

 Whether this alert could be deleted.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 When disabled the condition is not evaluated.  

 `FeatureArea`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The related feature area.  

 `FeatureGroup`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 FeatureGroup is a set of one or more feature areas.  

|||  
|-|-|  
|1|Administration|  
|2|Resources|  
|3|Deployment|  
|4|Monitoring|  
|5|Reporting|  

 `ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, key, read]  

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

 The name of alert.  

 `NumberOfSubscription`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of subscriptions to this alert.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The secured object type id.  

 `OccurrenceCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of times this alert has been activated.  

 `ParameterValues`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Values of administrator-defined parameters, such as thresholds, in XML format.  

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

|||  
|-|-|  
|0|Bad|  
|1|Good|  
|-1|Unknown|  

 `Severity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 The impact of this alert.  

|||  
|-|-|  
|1|Error|  
|2|Warning|  
|3|Informational|  

 `SkipUntil`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Evaluation will not start until the specified time.  

 `SourceSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The site code of the source site, only for some non-SLA alerts, NULL means it's a global SLA alert.  

 `TypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Identifier of this type of Alert.  

 `TypeInstanceID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User-defined identifier. The combination of TypeID and TypeInstanceID must be unique.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
