---
title: "SMS_BaselineAssignment Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: cf049dab-e45a-419e-bd26-1b92bbc77094searchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_BaselineAssignment Server WMI Class
The `SMS_BaselineAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains information about how a baseline is targeted.  

## Syntax  

```  
Class SMS_BaselineAssignment : SMS_CIAssignmentBaseClass  
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
      UInt32 LocaleID;  
      Boolean LogComplianceToWinEvent;  
      SInt32 NonComplianceCriticality;  
      Boolean NotifyUser;  
      Boolean OverrideServiceWindows;  
      SInt32 ParentAssignmentID;  
      Boolean RaiseMomAlertsOnFailure;  
      UInt32 RandomizationMinutes;  
      Boolean RebootOutsideOfServiceWindows;  
      Boolean SendDetailedNonComplianceStatus;  
      String SourceSite;  
      DateTime StartTime;   
      UInt32 StateMessagePriority;  
      UInt32 SuppressReboot;  
      String TargetCollectionID;  
      Boolean UseGMTTimes;  
      Boolean WoLEnabled;  
};  
```  

## Methods  
 The `SMS_BaselineAssignment` class does not define any methods.  

## Properties  
 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignedCI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Unique identifier of the assigned baseline configuration item.  

 `AssignedCIs`  
 Data type: `SInt32` Array  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentAction`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

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

 Qualifiers: [read, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `ContainsExpiredUpdates`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DesiredConfigType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DisableMomAlerts`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `DPLocality`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, bits]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `EnforcementDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [not_null, bits]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `EnforcementEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if enforcement is enabled.  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LogComplianceToWinEvent`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `NonComplianceCriticality`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `ParentAssignmentID`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 ParentAssignmentID  

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RandomizationMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Random time in minutes that is used when evaluating an assignment automatically once it arrives at the client. The random evaluation interval distributes the processing load when multiple assignments arrive at the client at same time.  

 `RebootOutsideOfServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `SendDetailedNonComplianceStatus`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

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

 `SuppressReboot`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, bits]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `WoLEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is used to define an assignment for a configuration baseline, which is a configuration item that contains other configuration items with associated rules. The baseline is assigned to computers through collections, together with a compliance evaluation schedule.  

 Your application can create a baseline as an [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md) object with the `CIType_ID` property set to Baseline (2). The types of configuration items that can be included in the baseline are:  

-   OperatingSystem (3)  

-   BusinessPolicy (4)  

-   Application (5)  

-   OtherConfigurationItem (7)  

 The baseline can reference configuration items of type SoftwareUpdate (1) and SoftwareUpdateBundle (2).  

 The [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md) object defines an `IsBundle` property. When building a baseline, this property of each contained configuration item is set to `true` to indicate that the configuration item is part of a bundle.  

 For information on the use of this class, see [How to List Configuration Assignments](../../../develop/compliance/how-to-list-configuration-assignments.md) and [How to Assign Configuration Baselines](../../../develop/compliance/how-to-assign-configuration-baselines.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)   
 [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md)
