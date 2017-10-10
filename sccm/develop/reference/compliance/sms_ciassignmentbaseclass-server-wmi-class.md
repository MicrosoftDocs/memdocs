---
title: "SMS_CIAssignmentBaseClass Class"
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
ms.assetid: 8d6a9e6e-f315-4527-90e3-514611e3431asearchScope: - ConfigMgr SDK
caps.latest.revision: 19
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CIAssignmentBaseClass Server WMI Class
The `SMS_CIAssignmentBaseClass` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as an abstract base class for the [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md) and [SMS_UpdatesAssignment Server WMI Class](../../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md).  

## Syntax  

```  
Class SMS_CIAssignmentBaseClass : SMS_BaseClass  
{  
      Boolean ApplyToSubTargets;  
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
      String EvaluationSchedule;  
      DateTime ExpirationTime;  
      DateTime LastModificationTime;  
      String LastModifiedBy;   
      UInt32 LocaleID;  
      Boolean LogComplianceToWinEvent;  
      SInt32 NonComplianceCriticality;  
      Boolean NotifyUser;  
      Boolean OverrideServiceWindows;  
      Boolean PersistOnWriteFilterDevices;  
      Boolean RaiseMomAlertsOnFailure;  
      Boolean RebootOutsideOfServiceWindows;  
      Boolean SendDetailedNonComplianceStatus;  
      Boolean SoftDeadlineEnabled;  
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
 The `SMS_CIAssignmentBaseClass` class does not define any methods.  

## Properties  
 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to apply the configuration item assignment to a subcollection.  

 This property is deprecated.  

 `AssignedCIs`  
 Data type: `SInt32` Array  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Array of IDs for the configuration items targeted by the assignment.  

 `AssignmentAction`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Action associated with the configuration item assignment. Possible values are:  

|||  
|-|-|  
|1|DETECT|  
|2|APPLY|  

 `AssignmentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The description of the configuration item assignment.  

 `AssignmentID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of the configuration item assignment. This ID is unique only for the site.  

 `AssignmentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The local assignment name.  

 `AssignmentType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of assignment. Possible values are:  

|||  
|-|-|  
|0|CIA_TYPE_DCM_BASELINE|  
|1|CIA_TYPE_UPDATES|  
|2|CIA_TYPE_APPLICATION|  
|5|CIA_TYPE_UPDATE_GROUP|  
|8|CIA_TYPE_POLICY|  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The unique ID of the configuration item assignment. This ID is unique across sites.  

 `ContainsExpiredUpdates`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 `true` if the deployment contains one or more expired updates.  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The date and time when the configuration item assignment is created.  

 `DesiredConfigType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The type of the configuration item. Possible values are:  

|||  
|-|-|  
|1|REQUIRED|  
|2|NOT_ALLOWED|  

 `DisableMomAlerts`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the client is configured to raise MOM alerts when a configuration item is applied. The default is `false`.  

 `DPLocality`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, bits]  

 Flags that determine how the client obtains distribution points, according to distribution point locality. Possible values are:  

 4  
 DP_DOWNLOAD_FROM_LOCAL  

 6  
 DP_DOWNLOAD_FROM_REMOTE  

 17  
 DP_NO_FALLBACK_UNPROTECTED  

 18  
 DP_ALLOW_WUMU  

 19  
 DP_ALLOW_METERED_NETWORK  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item assignment is enabled.  

 `EnforcementDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time when the configuration item assignment will be enforced.  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The assignment evaluation schedule.  

 `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time when the configuration item assignment expires.  

 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Date and time when the configuration item assignment was last modified.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User who last modified the configuration item.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 ID for the locale of the assignment name and assignment description properties.  

 `LogComplianceToWinEvent`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to log compliance status to Windows event logs. The default value is `false`.  

 `NonComplianceCriticality`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The configuration item non-compliance criticality for the assignment.  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to notify the user when a configuration item is available.  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the client ignores maintenance windows when a configuration item is applied.  

 `PersistOnWriteFilterDevices`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if write filters on devices should be persisted. The default value is `false`.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the client raises MOM alerts if it fails to apply a configuration item. The default is `false.`  

 `RebootOutsideOfServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the client reboots outside a maintenance window if a reboot is pending after applying a configuration item targeted by the assignment.  

 `SendDetailedNonComplianceStatus`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to send a detailed non-compliance status message. The default is `false`.  

 `SoftDeadlineEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable a soft deadline.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The site code of the site where the assignment was created.  

 `StateMessagePriority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [valuemap, values]  

 Priority of state message to be reported from client. The default value is 5.  

|||  
|-|-|  
|0|URGENT|  
|1|HIGH|  
|5|NORMAL|  
|10|LOW|  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The date and time when the configuration item assignment was initially offered.  

 `SuppressReboot`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, bits]  

 Value indicating whether the client should not reboot the computer, if there is a reboot pending after the configuration item is applied. Possible values are:  

|||  
|-|-|  
|0|SUPPRESS_REBOOT_WORKSTATIONS|  
|1|SUPPRESS_REBOOT_SERVERS|  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The ID of the collection to which the assignment is targeted.  

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the times and schedules are in Universal Coordinated Time (UTC).  

 `WoLEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to send a Wake On Lan (WoL) transmission to the client when the deadline is reached for the assignment.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)
