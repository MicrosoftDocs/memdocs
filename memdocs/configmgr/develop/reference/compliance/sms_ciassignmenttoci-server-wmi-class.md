---
title: SMS_CIAssignmentToCI Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a relationship between a configuration baseline and its assignments.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: edd1fa6e-d756-4805-94c0-8a3a5d428836
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CIAssignmentToCI Server WMI Class
The `SMS_CIAssignmentToCI` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a relationship between a configuration baseline and its assignments.  

## Syntax  

```  
Class SMS_CIAssignmentToCI : SMS_BaseClass  
{  
      UInt32 AssignmentID;  
      UInt32 CI_ID;  
};  
```  

## Methods  
 The `SMS_CIAssignmentToCI` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only.  

 Qualifiers: [key]  

 Unique ID of the assignment.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only.  

 Qualifiers: [key]  

 The unique ID of the configuration item. This ID is unique only for the site.  

## Remarks  
 Class qualifiers for this class include:  

- Association: ToInstance  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)
