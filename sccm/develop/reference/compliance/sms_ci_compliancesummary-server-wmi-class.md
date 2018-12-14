---
title: "SMS_CI_ComplianceSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 134d40db-3d25-4ff4-904f-3282c301d9c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CI_ComplianceSummary Server WMI Class
The `SMS_CI_ComplianceSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a compliance summary for a baseline configuration item.  

## Syntax  

```  
Class SMS_CI_ComplianceSummary : SMS_BaseClass  
{  
      UInt32 ActivatedCount;  
      UInt32 CI_ID;  
      String CI_UniqueID;  
      UInt32 CountCompliant;  
      UInt32 CountNoncompliant;  
      UInt32 CountTargeted;  
      UInt32 FailureCount;  
      DateTime LastSummaryTime;   
      String ModelName;  
      UInt32 Severity;  
};  
```  

## Methods  
 The `SMS_CI_ComplianceSummary` class does not define any methods.  

## Properties  
 `ActivatedCount`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of computers that evaluate the configuration item.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [unique]  

 The unique ID of the configuration item. This ID is unique across sites.  

 `CountCompliant`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of computers with which the configuration item is compliant.  

 `CountNoncompliant`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of computers with which the configuration item is not compliant.  

 `CountTargeted`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of computers that are targeted for the configuration item.  

 `FailureCount`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of computers that fail to evaluate the configuration item.  

 `LastSummaryTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 Date and time when the summary task was last run.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model Name of the configuration item.  

 `Severity`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The noncompliance severity reported by the client for the configuration item.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class for compliance monitoring for a configuration item.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
