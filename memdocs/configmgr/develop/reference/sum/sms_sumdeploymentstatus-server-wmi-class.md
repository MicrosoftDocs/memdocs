---
title: "SMS_SUMDeploymentStatus Class"
titleSuffix: "Configuration Manager"
description: "The SMS_SUMDeploymentStatus WMI class represents per-deployment-state summary for SUM deployments in-console monitoring."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f263eddd-b038-429c-b052-b69c18351d79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SUMDeploymentStatus Server WMI Class
The `SMS_SUMDeploymentStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents per-deployment-state summary for SUM deployments in-console monitoring.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SUMDeploymentStatus : SMS_BaseClass  
{  
    UInt32 Assets;  
    UInt32 AssignmentID;  
    String AssignmentName;  
    String AssignmentUniqueID;  
    String CollectionID;  
    String CollectionName;  
    DateTime LastStatusTime;  
    String StatusDescription;  
    UInt32 StatusEnforcementState;  
    UInt32 StatusErrorCode;  
    UInt32 StatusType;  
    DateTime SummarizationTime;  
};  
```  

## Methods  
 The `SMS_SUMDeploymentStatus` class does not define any methods.  

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

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last status time.  

 `StatusDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the status.  

 `StatusEnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Additional enforcement state for progress and error status (0 for others).  

 `StatusErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Additional error code for error status (0 for others).  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, key, read]  

 Status type. Possible values are:  

| Value | Status |  
| ----- | ------ |  
|1|Success|  
|2|InProgress|  
|4|Unknown|  
|5|Error|  

 `SummarizationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The last time the summarization task was run for this application.  

## Remarks  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
