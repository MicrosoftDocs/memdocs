---
title: "SMS_DCMDeploymentCompliantDetailsPerAsset Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 73bc9f0b-e30e-475e-8424-21fadbbdc993
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class
The `SMS_DCMDeploymentCompliantDetailsPerAsset` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentCompliantDetailsPerAsset : SMS_BaseClass  
{  
    String ADUserName;  
    UInt32 AssetID;  
    UInt32 AssetType;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    UInt32 BL_ID;  
    String BLName;  
    UInt32 BLRevision;  
    UInt32 CI_ID;  
    String CIName;  
    UInt32 ClientType;  
    String ClientTypeDisplay;  
    String DeviceName;  
    String DiscoveredValue;  
    String InstanceData;  
    Boolean IsBaselineRule;  
    UInt32 ItemKey;  
    String PreviousValue;  
    UInt32 Revision;  
    UInt32 Rule_ID;  
    String RuleDescription;  
    String RuleName;  
    String RuleStateDisplay;  
    String RuleSubStateDisplay;  
    UInt32 Setting_ID;  
    String SettingDescription;  
    String SettingName;  
    UInt32 StatusType;  
    UInt32 SubStatusType;  
    String TargetCollectionID;  
    String ValidationRule;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentCompliantDetailsPerAsset` class does not define any methods.  

## Properties  
 `ADUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Active Directory user name.  

 `AssetID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the asset.  

 `AssetType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 Type of the asset. Possible values are:  

|Value|Asset type|  
|-|-|  
|0|USER|  
|1|MACHINE|  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The assignment ID.

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the configuration item assignment. This ID is unique only for the site.  

 `BL_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Baseline database identifier that is deployed using this assignment.  

 `BLName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Baseline name that is deployed using this assignment.  

 `BLRevision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Baseline version that is deployed using this assignment.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CIName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the configuration item.  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 Type of client. Possible values are:  

|Value|Client type|  
|-|-|  
|1|WINDOWS_CLIENT|  
|2|WINDOWS_MOBILE|  

 `ClientTypeDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the client type in the console.  

 `DeviceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the device of the targeted asset.  

 `DiscoveredValue`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Value of the setting that was discovered and reported when the rule is non-compliant.  

 `InstanceData`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Discovered path of the instance of the setting being referenced by the non-compliant rule.  

 `IsBaselineRule`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this is a baseline rule.  

 `ItemKey`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Database identifier of the asset being reported for.  

 `PreviousValue`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Value of the setting discovered during the prior evaluation of the baseline.  

 `Revision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Version of the baseline deployed using this assignment.  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The database identifier of a rule defined in a configuration item.  

 `RuleDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Descriptive name that identifies the rule.  

 `RuleName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the rule.  

 `RuleStateDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Represents the state of the rule reported by the asset. Possible values are:  

|Value|
|-|  
|Compliant|  
|Non-compliant|  
|Error|  
|Conflict|  

 `RuleSubStateDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Represents the sub state of the rule reported by the asset. Possible values are:  

|Value|
|-|  
|Not-Applicable|  
|Not-Detected|  

 `Setting_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Database identifier of a setting in the configuration item.  

 `SettingDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of a setting in the configuration item.  

 `SettingName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of a setting in the configuration item.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Status of the deployment to the targeted asset. Possible values are:  

|Value|Deployment status|  
|-|-|  
|1|Success|  
|2|InProgress|  
|4|Unknown|  

 `SubStatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Substatus type. Possible values are:  

|Value|Substatus type|  
|-|-|  
|0|Compliant|  
|1|Not-Applicable|  
|2|Not-Detected|  
|3|Enforced|  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the collection to which the assignment is targeted.  

 `ValidationRule`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The validation criteria defined for the rule in the configuration item.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
