---
title: SMS_DCMDeploymentErrorDetailsPerAsset Class
titleSuffix: Configuration Manager
description: The SMS_DCMDeploymentErrorDetailsPerAsset WMI class is an SMS Provider server class that represents asset details per asset for a deployment error.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: dd567a31-8780-48e0-8566-61f744d52e8f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DCMDeploymentErrorDetailsPerAsset Server WMI Class
The `SMS_DCMDeploymentErrorDetailsPerAsset` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents asset details per asset for a deployment error.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentErrorDetailsPerAsset : SMS_BaseClass  
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
    UInt32 ErrorCode;  
    String ErrorDescription;  
    UInt32 ErrorType;  
    String ErrorTypeDisplay;  
    UInt32 ItemKey;  
    String ObjectDescription;  
    UInt32 ObjectID;  
    String ObjectName;  
    UInt32 ObjectType;  
    String ObjectTypeName;  
    UInt32 Revision;  
    String RuleStateDisplay;  
    UInt32 StatusType;  
    String TargetCollectionID;  
    String ValidationRule;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentErrorDetailsPerAsset` class does not define any methods.  

## Properties  
 `ADUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `AssetID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the asset.  

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

 Qualifiers: [enumeration, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ClientTypeDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `DeviceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Error code.  

 `ErrorDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the error.  

 `ErrorType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Error type. Possible values are:  

|Value|Error type|  
|-|-|  
|1|INFRASTRUCTURAL|  
|2|DISCOVERY|  
|3|CONFLICT|  
|4|ENFORCEMENT|  

 `ErrorTypeDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the error type in the console.  

 `ItemKey`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `ObjectDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the object.  

 `ObjectID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 ID of the object.  

 `ObjectName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the object.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Object type. Possible values are:  

|Value|Object type|  
|-|-|  
|1|CI|  
|2|SETTING|  
|3|RULE|  

 `ObjectTypeName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the object type.  

 `Revision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

 `RuleStateDisplay`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md).  

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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
