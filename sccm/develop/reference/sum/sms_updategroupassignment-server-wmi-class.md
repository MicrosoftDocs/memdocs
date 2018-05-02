---
title: "SMS_UpdateGroupAssignment Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e0f59acd-8dbc-42b4-aaef-8261c4860577
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UpdateGroupAssignment Server WMI Class
The `SMS_UpdateGroupAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a deployment of an update group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdateGroupAssignment : SMS_CIAssignmentBaseClass  
{  
    Boolean ApplyToSubTargets;  
    SInt32 AssignedCIs[];  
    SInt32 AssignedUpdateGroup;  
    SInt32 AssignmentAction;  
    String AssignmentDescription;  
    SInt32 AssignmentID;  
    String AssignmentName;  
    SInt32 AssignmentType;  
    String AssignmentUniqueID;  
    Boolean ContainsExpiredUpdates;  
    DateTime CreationTime;  
    SInt32 DesiredConfigType;  
    Boolean DisableMomAlerts;  
    UInt32 DPLocality;  
    Boolean Enabled;  
    DateTime EnforcementDeadline;  
    String EvaluationSchedule;  
    DateTime ExpirationTime;  
    DateTime LastModificationTime;  
    String LastModifiedBy;  
    Boolean LimitStateMessageVerbosity; (obsolete in SP1)  
    UInt32 LocaleID;  
    Boolean LogComplianceToWinEvent;  
    SInt32 NonComplianceCriticality;  
    Boolean NotifyUser;  
    Boolean OverrideServiceWindows;  
    Boolean RaiseMomAlertsOnFailure;  
    Boolean RandomizationEnabled;  
    Boolean RebootOutsideOfServiceWindows;  
    Boolean SendDetailedNonComplianceStatus;  
    String SourceSite;  
    DateTime StartTime;  
    UInt32 StateMessagePriority;  
    UInt32 StateMessageVerbosity;  
    UInt32 SuppressReboot;  
    String TargetCollectionID;  
    Boolean UseBranchCache;  
    Boolean UseGMTTimes;  
    Boolean UserUIExperience;  
    Boolean WoLEnabled;  
};  
```  

## Methods  
 The `SMS_UpdateGroupAssignment` class does not define any methods.  

## Properties  
 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [deprecated]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignedCIs`  
 Data type: `SInt32 Array`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignedUpdateGroup`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 AssignedUpdateGroup description … .  

 `AssignmentAction`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null, enumeration, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key, key]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `ContainsExpiredUpdates`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DesiredConfigType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null, enumeration, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DisableMomAlerts`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DPLocality`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits, not_null, bits, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `EnforcementDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See the SMS_CIAssignmentBaseClass Server WMI Class.  

 `LimitStateMessageVerbosity`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `LimitStateMessageVerbosity` is deprecated in SP1. However, the value must still remain synchronized with `StateMessageVerbosity`. For `StateMessageVerbosity` values < 10, `LimitStateMessageVerbosity` must be set to `true`, otherwise `LimitStateMessageVerbosity` must be set to `false`.  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LogComplianceToWinEvent`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `NonComplianceCriticality`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)..  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RandomizationEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 RandomizationEnabled.   

 `RebootOutsideOfServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `SendDetailedNonComplianceStatus`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `StateMessagePriority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `StateMessageVerbosity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Verbosity of state messages sent for this deployment.  

|||  
|-|-|  
|0|NONE|  
|1|ERRORS|  
|5|SUCCESSES|  
|10|ALL|  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `SuppressReboot`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `UseBranchCache`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 UseBranchCache description … .   

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `UserUIExperience`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 UserUIExperience description … .  

 `WoLEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
