---
title: "SMS_DCMDeploymentErrorAssetDetails Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 5b0c3b0c-bb1c-4e2d-a1ff-5a7d06c23c72
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DCMDeploymentErrorAssetDetails Server WMI Class
The `SMS_DCMDeploymentErrorAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the asset details for deployment error.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentErrorAssetDetails : SMS_BaseClass  
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
    UInt32 ErrorCode;  
    String ErrorDescription;  
    UInt32 ErrorType;  
    String ErrorTypeDisplay;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    String ObjectDescription;  
    UInt32 ObjectID;  
    String ObjectName;  
    UInt32 ObjectType;  
    String ObjectTypeName;  
    UInt32 Revision;  
    String RuleStateDisplay;  
    UInt32 StatusType;  
    String TargetCollectionID;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentErrorAssetDetails` class does not define any methods.  

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

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Error code.  

 `ErrorDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the error.  

 `ErrorType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, key, not_null, read]  

 Error type. Possible values are:  

|||  
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

 `true` if this is a virtual machine.  

 `ObjectDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the object.  

 `ObjectID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Ihow tD of the object.  

 `ObjectName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the object.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, key, not_null, read]  

 Object type. Possible values are:  

|||  
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

 Version of the baseline deployed using this assignment.  

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
