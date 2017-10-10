---
title: "SMS_SUMDeploymentAssetDetails Class"
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
ms.assetid: 6890fa15-c9c0-4c35-aee0-dc5d373e63e2searchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SUMDeploymentAssetDetails Server WMI Class
The `SMS_SUMDeploymentAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents per-asset details for SUM deployments in-console monitoring.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SUMDeploymentAssetDetails : SMS_BaseClass  
{  
    UInt32 AssignmentID;  
    String AssignmentName;  
    String AssignmentUniqueID;  
    String CollectionID;  
    String CollectionName;  
    String DeviceName;  
    UInt32 IsCompliant;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    String LastComplianceMessageDesc;  
    UInt32 LastComplianceMessageID;  
    DateTime LastComplianceMessageTime;  
    UInt32 LastEnforcementErrorCode;  
    UInt32 LastEnforcementErrorID;  
    DateTime LastEnforcementErrorTime;  
    String LastEnforcementMessageDesc;  
    UInt32 LastEnforcementMessageID;  
    DateTime LastEnforcementMessageTime;  
    UInt32 ResourceID;  
    String StatusDescription;  
    UInt32 StatusEnforcementState;  
    UInt32 StatusErrorCode;  
    DateTime StatusTime;  
    UInt32 StatusType;  
    String UserID;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_SUMDeploymentAssetDetails` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The ID of the configuration item assignment. This ID is unique only for the site.  

 `AssignmentName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The local assignment name.  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The unique ID of the configuration item assignment. This ID is unique across sites.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Existing collection to which the deployment is being targeted.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the collection to which the deployment is being targeted.  

 `DeviceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the device.  

 `IsCompliant`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the asset is compliant.  

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

 `LastComplianceMessageDesc`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last Compliance Message Description.  

 `LastComplianceMessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last compliance message ID.  

 `LastComplianceMessageTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last compliance message time.  

 `LastEnforcementErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement error code.  

 `LastEnforcementErrorID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement error ID.  

 `LastEnforcementErrorTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement error time.  

 `LastEnforcementMessageDesc`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement message description.  

 `LastEnforcementMessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement message ID.  

 `LastEnforcementMessageTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last enforcement message time.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Unique Configuration Manager-supplied ID for the resource.  

 `StatusDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the status.  

 `StatusEnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Additional enforcement state for progress and error status (0 for others).  

 `StatusErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Additional error code for error status (0 for others).  

 `StatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status time.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 Status type. Possible values are:  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|4|Unknown|  
|5|Error|  

 `UserID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Identifier of the user.  

 `VMHostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of virtual machine host.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)   
 [Configuration Manager Software Updates](../../../develop/sum/software-updates.md)
