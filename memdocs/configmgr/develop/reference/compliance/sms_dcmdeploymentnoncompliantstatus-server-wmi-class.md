---
title: "SMS_DCMDeploymentNonCompliantStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 67caab62-edaf-4904-85b6-452811188c03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DCMDeploymentNonCompliantStatus Server WMI Class
The `SMS_DCMDeploymentNonCompliantStatus` Windows Management Instrumentation (WMI)  class is an SMS Provider server class, in Configuration Manager, that represents non-compliant status for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentNonCompliantStatus : SMS_BaseClass  
{  
    UInt32 Assets;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    UInt32 BL_ID;  
    String BLName;  
    UInt32 BLRevision;  
    UInt32 CI_ID;  
    String CIName;  
    DateTime DeploymentTime;  
    Boolean IsBaselineRule;  
    UInt32 Revision;  
    UInt32 Rule_ID;  
    String RuleDescription;  
    String RuleName;  
    UInt32 RuleSeverity;  
    String RuleStateDisplay;  
    UInt32 RuleSubState;  
    UInt32 StatusType;  
    DateTime SummarizationTime;  
    UInt32 SummaryType;  
    String TargetCollectionID;  
    String ValidationRule;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentNonCompliantStatus` class does not define any methods.  

## Properties  
 `Assets`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Number of assets related to the status.  

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

 `DeploymentTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Deployment time.  

 `IsBaselineRule`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

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

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

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

 Rule sub-status type. .  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `SummarizationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Summarization time.   

 `SummaryType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Summary type.   

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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
