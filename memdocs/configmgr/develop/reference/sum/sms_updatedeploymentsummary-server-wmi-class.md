---
title: "SMS_UpdateDeploymentSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c9c0923f-9ec6-463c-905b-59fb515b1dfb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_UpdateDeploymentSummary Server WMI Class
The `SMS_UpdateDeploymentSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a summary for a given software update in given software updates deployment.  

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

 This property is deprecated in Configuration Manager.  

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

- Secured  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
