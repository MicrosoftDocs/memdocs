---
title: "SMS_UpdatesAssignment Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_UpdatesAssignment WMI class is an SMS Provider server class that represents a deployment."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e470bca9-d185-4d49-80c7-47802c515cf7
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# SMS_UpdatesAssignment Server WMI Class
The `SMS_UpdatesAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdatesAssignment : SMS_CIAssignmentBaseClass  
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
 The `SMS_UpdatesAssignment` class does not define any methods.  

## Properties  
 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

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

 For this class, the default value is APPLY (2).  

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

 Access type: Read  

 Qualifiers: None  

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

 For this class, the default value is REQUIRED (1).  

| Value | Type |  
| ----- | ---- |  
|1|REQUIRED|  
|2|NOT_ALLOWED|  

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

 For this class, the `DPLocality` property defaults to the flag combination DP_DOWNLOAD_FROM_LOCAL &#124; DP_DOWNLOAD_FROM_REMOTE (0x50).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `EnforcementDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time to automatically install the software update. Set this property to zero if the update is optional. It must not be set to a null pointer.  

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

 Access type: Read-only  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `LimitStateMessageVerbosity`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `LimitStateMessageVerbosity` is deprecated in SP1. However, the value must still remain synchronized with `StateMessageVerbosity`. For `StateMessageVerbosity` values < 10, `LimitStateMessageVerbosity` must be set to `true`, otherwise `LimitStateMessageVerbosity` must be set to `false`.  

 This method/property has been removed or deprecated in Configuration Manager SP1.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

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

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RandomizationEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 The post-deadline randomization delay was introduced in System Center 2012 Configuration Manager to better support virtual desktop infrastructure (VDI) environments and large-scale client deployments. The default post-deadline randomization delay is 120 minutes. Setting RandomizationEnabled to false disables the randomization delay.   

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

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `StateMessageVerbosity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Verbosity of state messages sent for this deployment.  

| Value | Message verbosity |  
| ----- | ----------------- |  
|0|NONE|  
|1|ERRORS|  
|5|SUCCESSES|  
|10|ALL|  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

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

 `UseBranchCache`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Use branch cache. The default value is `true`.  

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `UserUIExperience`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to show a reboot notification. When set to `false`, no reboot notification will be shown. The default value is `true`.  

 `WoLEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  After preparing the software updates to deploy, your application can use this class as described in How to Configure and Deploy Updates. After the application creates the deployment, Configuration Manager creates the corresponding policy in the database. The client polls the management point for new and changed properties and the download occurs when a request is detected.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
