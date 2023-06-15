---
description: Learn how to use the  SMS_ConfigurationPolicyAssignment to represent the deployment of an instance of SMS_ConfigurationPolicy in Configuration Manager.
title: SMS_ConfigurationPolicyAssignment Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: eb3f5212-bc83-403a-b684-aa3339364729
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ConfigurationPolicyAssignment Server WMI Class
The `SMS_ConfigurationPolicyAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the deployment of an instance of `SMS_ConfigurationPolicy`. It is similar to `SMS_BaselineAssignment`, except that `SMS_ConfigurationPolicy` is deployed directly, instead of being collected into a baseline first.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationPolicyAssignment : SMS_CIAssignmentBaseClass  
{  
    Boolean ApplyToSubTargets;  
    String AssignedCI_UniqueID;  
    SInt32 AssignedCIs[];  
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
    Boolean EnforcementEnabled;  
    String EvaluationSchedule;  
    DateTime ExpirationTime;  
    DateTime LastModificationTime;  
    String LastModifiedBy;  
    Boolean LimitStateMessageVerbosity;  
    UInt32 LocaleID;  
    Boolean LogComplianceToWinEvent;  
    SInt32 NonComplianceCriticality;  
    Boolean NotifyUser;  
    Boolean OverrideServiceWindows;  
    Boolean PersistOnWriteFilterDevices;  
    Boolean RaiseMomAlertsOnFailure;  
    UInt32 RandomizationMinutes;  
    Boolean RebootOutsideOfServiceWindows;  
    Boolean SendDetailedNonComplianceStatus;  
    String SourceSite;  
    DateTime StartTime;  
    UInt32 StateMessagePriority;  
    UInt32 StateMessageVerbosity;  
    UInt32 SuppressReboot;  
    String TargetCollectionID;  
    Boolean UseGMTTimes;  
    Boolean UserUIExperience;  
    Boolean WoLEnabled;  
};  
```  

## Methods  
 The `SMS_ConfigurationPolicyAssignment` class does not define any methods.  

## Properties  
 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [deprecated]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignedCI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Unique identifier of the assigned baseline configuration item.  

 `AssignedCIs`  
 Data type: `SInt32 Array`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignmentAction`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignmentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key, key]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignmentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignmentType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `ContainsExpiredUpdates`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `DesiredConfigType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `DisableMomAlerts`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `DPLocality`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `EnforcementDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `EnforcementEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md).  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `LimitStateMessageVerbosity`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, obsoleted]  

 This method/property has been removed or deprecated in Configuration Manager SP1.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `LogComplianceToWinEvent`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `NonComplianceCriticality`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `PersistOnWriteFilterDevices`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `RandomizationMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Random time in minutes that is used when evaluating an assignment automatically once it arrives at the client. The random evaluation interval distributes the processing load when multiple assignments arrive at the client at same time.  

 `RebootOutsideOfServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `SendDetailedNonComplianceStatus`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `StateMessagePriority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `StateMessageVerbosity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 See [SMS_UpdateGroupAssignment Server WMI Class](../../../develop/reference/sum/sms_updategroupassignment-server-wmi-class.md).  

 `SuppressReboot`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

 `UserUIExperience`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if user notification is displayed; otherwise, `false`.  

 `WoLEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
