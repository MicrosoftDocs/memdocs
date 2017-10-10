---
title: "SMS_AppDeploymentAssetDetails Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 32952cd0-65f7-4106-9e58-8392d9ef0c6bsearchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AppDeploymentAssetDetails Server WMI Class
The `SMS_AppDeploymentAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents asset-level details about the deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppDeploymentAssetDetails : SMS_BaseClass  
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
    UInt64 DTResultID;  
    UInt32 EnforcementState;  
    UInt32 ExtendedInfoDescriptionID;  
    UInt32 ExtendedInfoID;  
    UInt32 InstalledState;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    UInt32 MachineID;  
    String MachineName;  
    UInt32 PolicyModelID;  
    UInt32 Revision;  
    DateTime StartTime;  
    UInt32 StatusType;  
    String Technology;  
    UInt32 UpdateState;  
    String UserName;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_AppDeploymentAssetDetails` class does not define any methods.  

## Properties  
 `AppCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Application configuration item.  

 `AppName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Application description.  

 `AppStatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Application status type. Possible values are:  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|RequirementsNotMet|  
|4|Unknown|  
|5|Error|  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md).  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 ID of the collection to which the deployment was deployed.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Collection name.  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Compliance state for the configuration item.  

 `DeploymentIntent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Intended purpose of the deployment. Possible values are:  

|||  
|-|-|  
|1|Install|  
|2|Uninstall|  
|3|Preflight|  

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Deployment type configuration item.  

 `DTModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Deployment Type Model ID.  

 `DTName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the deployment type.  

 `DTResultID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Deployment Type Result ID.  

 `EnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The enforcement state. Possible values are:  

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

 `ExtendedInfoDescriptionID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Extended information description ID.  

 `ExtendedInfoID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Extended information ID.  

 `InstalledState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Installed state. Possible values are:  

|||  
|-|-|  
|1|Uninstall|  
|2|Install|  
|3|Unknown|  

 `IsMachineAssignedToUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the computer is assigned to a user.  

 `IsMachineChangesPersisted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if changes made to virtual machine  are persisted.  

 `IsVM`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the computer is a virtual machine.  

 `MachineID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 ID of the virtual machine.  

 `MachineName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Virtual machine name.  

 `PolicyModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Policy Model ID.  

 `Revision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Revision.  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Deployment time.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status type.  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|RequirementsNotMet|  
|4|Unknown|  
|5|Error|  

 `Technology`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Technology.  

 `UpdateState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Update state.  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 User name.  

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
