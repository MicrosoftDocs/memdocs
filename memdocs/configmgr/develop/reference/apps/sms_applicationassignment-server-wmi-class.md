---
title: SMS_ApplicationAssignment Class
titleSuffix: Configuration Manager
description: The SMS_ApplicationAssignment WMI class represents the assignment of an application to a collection. 
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d4022814-fd1f-4c85-b6e2-787aa3f94953
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ApplicationAssignment Server WMI Class
The `SMS_ApplicationAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the assignment of an application to a collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ApplicationAssignment : SMS_CIAssignmentBaseClass  
{  
    String ApplicationName;  
    Boolean ApplyToSubTargets;  
    UInt32 AppModelID;  
    String AssignedCI_UniqueID;  
    SInt32 AssignedCIs[];  
    SInt32 AssignmentAction;  
    String AssignmentDescription;  
    SInt32 AssignmentID;  
    String AssignmentName;  
    SInt32 AssignmentType;  
    String AssignmentUniqueID;  
    String CollectionName;  
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
    UInt32 OfferFlags;  
    SInt32 OfferTypeID;  
    Boolean OverrideServiceWindows;  
    SMS_ApplicationPolicyTemplateBinding PolicyBinding[];  
    SInt32 Priority;  
    Boolean RaiseMomAlertsOnFailure;  
    Boolean RebootOutsideOfServiceWindows;  
    Boolean RequireApproval;  
    Boolean SendDetailedNonComplianceStatus;  
    String SourceSite;  
    DateTime StartTime;  
    UInt32 StateMessagePriority;  
    UInt32 SuppressReboot;  
    String TargetCollectionID;  
    DateTime UpdateDeadline;  
    Boolean UpdateSupersedence;  
    Boolean UseGMTTimes;  
    Boolean UserUIExperience;  
    Boolean WoLEnabled;  
};  
```  

## Methods  
 The `SMS_ApplicationAssignment` class does not define any methods.  

## Properties  
 `ApplicationName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [readonly]  

 Name of the application.  

 `ApplyToSubTargets`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [deprecated]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AppModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [readonly]  

 AppModelID description.  

 `AssignedCI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignedCIs`  
 Data type: `SInt32 Array`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

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

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [readonly]  

 Name of the collection to which the deployment was deployed.  

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

 Qualifiers: [bits, not_null]  

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

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

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

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `OfferFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits, not_null]  

 Offer flags. Possible values are:  

|Value|Offer flag|  
|-|-|  
|1|PREDEPLOY|  
|2|ONDEMAND|  
|4|ENABLEPROCESSTERMINATION|  
|8|ALLOWUSERSTOREPAIRAPP|  
|16|RELATIVESCHEDULE|  
|32|HIGHIMPACTDEPLOYMENT|  

 `OfferTypeID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null]  

 Type of offer. Possible values are:  

|Value|Offer type|  
|-|-|  
|0|REQUIRED|  
|2|AVAILABLE|  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `PolicyBinding`  
 Data type: `SMS_ApplicationPolicyTemplateBinding Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The dynamic binding of an application policy to a deployment type.  

 `Priority`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, not_null]  

 Priority for installation of the application. Possible values are:  

|Value|Installation priority|  
|-|-|  
|0|LOW|  
|1|MEDIUM|  
|2|HIGH|  

 `RaiseMomAlertsOnFailure`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RebootOutsideOfServiceWindows`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `RequireApproval`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the request for this user-available assignment requires approval from the administrator.  

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

 `UpdateDeadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Deadline for updates.  

 `UpdateSupersedence`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if you should update the supersedence; otherwise, `false`.  

 `UseGMTTimes`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `UserUIExperience`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if user notification is displayed; otherwise, `false`.  

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
