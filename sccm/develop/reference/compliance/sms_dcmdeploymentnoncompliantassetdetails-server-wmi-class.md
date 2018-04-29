---
title: "SMS_DCMDeploymentNonCompliantAssetDetails Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: da079cfb-c148-4b38-9173-307843dc0b90
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DCMDeploymentNonCompliantAssetDetails Server WMI Class
The `SMS_DCMDeploymentNonCompliantAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents non-compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentNonCompliantAssetDetails : SMS_BaseClass  
{  
    UInt32 AssetID;  
    String AssetName;  
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
    Boolean IsBaselineRule;  
    Boolean IsEnforced;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    UInt32 Revision;  
    UInt32 Rule_ID;  
    String RuleDescription;  
    String RuleName;  
    UInt32 RuleSeverity;  
    String RuleStateDisplay;  
    UInt32 RuleSubState;  
    UInt32 StatusType;  
    String TargetCollectionID;  
    String ValidationRule;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentNonCompliantAssetDetails` class does not define any methods.  

## Properties  
 `AssetID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `AssetName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of the asset.  

 `AssetType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `BL_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `BLName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `BLRevision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `CIName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ClientTypeDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `IsBaselineRule`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `IsEnforced`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this is enforced.  

 `IsMachineAssignedToUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the computer is assigned to a user.  

 `IsMachineChangesPersisted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the virtual machine changes are persisted.  

 `IsVM`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this is a virtual machine. True, if this is a virtual machine.  

 `Revision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `RuleDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `RuleName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the rule.  

 `RuleSeverity`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Severity of the rule.  

 `RuleStateDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `RuleSubState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Rule sub-state.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ValidationRule`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `VMHostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Virtual machine host name.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
