---
title: "SMS_AppDeploymentRequirementsNotMetStatus Class"
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
ms.assetid: efaa6ef5-e9a0-4939-bf9a-855e42d2df65searchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AppDeploymentRequirementsNotMetStatus Server WMI Class
The `SMS_AppDeploymentRequirementsNotMetStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the status of application deployment where requirements are not met.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppDeploymentRequirementsNotMetStatus : SMS_BaseClass  
{  
    UInt32 AppCI;  
    String AppName;  
    UInt32 AppStatusType;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    String CollectionName;  
    UInt32 DeploymentIntent;  
    UInt32 DTCI;  
    UInt32 DTModelID;  
    String DTName;  
    UInt32 EnforcementState;  
    UInt32 PolicyModelID;  
    String RequirementName;  
    UInt32 RequirementType;  
    UInt32 RuleID;  
    DateTime StartTime;  
    UInt32 StatusType;  
    String Technology;  
    UInt32 Total;  
};  
```  

## Methods  
 The `SMS_AppDeploymentRequirementsNotMetStatus` class does not define any methods.  

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

 Enforcement state. Possible values are:  

|||  
|-|-|  
|0|Enforcement State Unknown|  
|1|Enforcement started|  
|2|Enforcement waiting for content|  
|3|Waiting for another installation to complete|  
|4|Waiting for maintenance window before installing|  
|5|Restart required before installing|  
|6|General failure|  
|7|Pending installation|  
|8|Installing update|  
|9|Pending system restart|  
|10|Successfully installed update|  
|11|Failed to install update|  
|12|Downloading update|  
|13|Downloaded update|  
|14|Failed to download update|  

 `PolicyModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `RequirementName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the requirement.  

 `RequirementType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Type of requirement that has not been met. Possible values are:  

|||  
|-|-|  
|0|Constraint violation|  
|1|Conflict violation|  
|2|Enforcement violation|  
|3|Requirement violation|  
|4|Dependency violation|  

 `RuleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Rule ID of the requirement that has not been met.  

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

 Status type.  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|4|Unknown|  
|5|Error|  

 `Technology`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `Total`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Total number of systems that do not meet the requirements.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
