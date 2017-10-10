---
title: "SMS_UpdateDeploymentSummary Class"
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
ms.assetid: c9c0923f-9ec6-463c-905b-59fb515b1dfbsearchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UpdateDeploymentSummary Server WMI Class
The `SMS_UpdateDeploymentSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a summary for a given software update in given software updates deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdateDeploymentSummary : SMS_BaseClass  
{  
      Boolean AssignmentEnabled;  
      UInt32 AssignmentID;  
      String AssignmentName;  
      String AssignmentUniqueID;  
      UInt32 CI_ID;  
      String CollectionID;  
      String CollectionName;  
      Boolean IncludeSubCollections;  
      UInt32 NumFailed;  
      UInt32 NumInstalled;  
      UInt32 NumMissing;  
      UInt32 NumNotApplicable;  
      UInt32 NumPresent;  
      UInt32 NumTotal;  
      UInt32 NumUnknown;  
      DateTime StartTime;  
};  
```  

## Methods  
 The `SMS_UpdateDeploymentSummary` class does not define any methods.  

## Properties  
 `AssignmentEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the assignment is enabled.  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The ID for the configuration item assignment.  

 `AssignmentName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The name of the configuration item assignment.  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The unique ID of the configuration item assignment.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The ID of the software update configuration item. This ID is only unique for the site.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The ID for the collection associated with the update deployment.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The name of the collection associated with the update deployment.  

 `IncludeSubCollections`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 This property is deprecated in System Center Configuration Manager.  

 `NumFailed`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the configuration item installation failed.  

 `NumInstalled`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the configuration item was installed by enforcement.  

 `NumMissing`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the configuration item is missing.  

 `NumNotApplicable`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the configuration item is not applicable.  

 `NumPresent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the configuration item is already installed.  

 `NumTotal`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Total number of computers in the collection.  

 `NumUnknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 Number of computers for which the state of the configuration item is unknown.  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The date and time when the assignment was initially offered.  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)   
 [Configuration Manager Software Updates](../../../develop/sum/software-updates.md)
