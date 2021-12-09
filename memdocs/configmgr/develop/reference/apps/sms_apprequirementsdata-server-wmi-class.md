---
title: "SMS_AppRequirementsData Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ce91d315-6baa-40aa-a944-2458131e5087
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_AppRequirementsData Server WMI Class
The `SMS_AppRequirementsData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the requirements data of an application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppRequirementsData : SMS_BaseClass  
{  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    UInt32 DTCI;  
    UInt64 DTResultID;  
    UInt32 InstanceGroup;  
    String MachineName;  
    String RequirementName;  
    UInt32 RuleID;  
    String SettingName;  
    String SettingValue;  
    String UniqueRequirementName;  
    String UserName;  
};  
```  

## Methods  
 The `SMS_AppRequirementsData` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTResultID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `InstanceGroup`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Instance group.  

 `MachineName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `RequirementName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the requirement.  

 `RuleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Identifier of the rule.  

 `SettingName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of the setting.  

 `SettingValue`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Setting value.  

 `UniqueRequirementName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Unique requirement name.  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
