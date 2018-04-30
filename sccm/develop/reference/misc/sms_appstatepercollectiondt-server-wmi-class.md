---
title: "SMS_AppStatePerCollectionDT Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d7f92b65-9bc7-4a39-b610-abadf9e3d6fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AppStatePerCollectionDT Server WMI Class
The `SMS_AppStatePerCollectionDT` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application state per collection deployment type.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppStatePerCollectionDT : SMS_BaseClass  
{  
    UInt32 AppCI;  
    String AppName;  
    UInt32 AppStatusType;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    String CollectionName;  
    UInt32 ComplianceState;  
    UInt32 DeploymentIntent;  
    UInt32 DTCI;  
    UInt32 DTModelID;  
    String DTName;  
    UInt32 EnforcementState;  
    String RequirementName;  
    UInt32 RequirementType;  
    DateTime StartTime;  
    UInt32 StatusType;  
    String Technology;  
    UInt32 Total;  
};  
```  

## Methods  
 The `SMS_AppStatePerCollectionDT` class does not define any methods.  

## Properties  
 `AppCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AppName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AppStatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DeploymentIntent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `EnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `RequirementName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of requirement.   

 `RequirementType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Type of requirement.   

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `Technology`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `Total`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Total.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
