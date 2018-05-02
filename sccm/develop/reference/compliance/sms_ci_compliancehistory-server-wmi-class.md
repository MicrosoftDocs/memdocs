---
title: "SMS_CI_ComplianceHistory Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c37551e3-f22b-42e5-9943-858fb58acdf0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CI_ComplianceHistory Server WMI Class
The `SMS_CI_ComplianceHistory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides the compliance history for both configuration items and configuration baselines.  

## Syntax  

```  
Class SMS_CI_ComplianceHistory : SMS_BaseClass  
{  
      UInt32 CI_ID;  
      String CI_UniqueID;  
      UInt32 CIVersion;   
      DateTime ComplianceEndDate;  
      DateTime ComplianceStartDate;  
      UInt32 ComplianceValidationRuleFailures;  
      UInt32 DesiredState;  
      Boolean IsApplicable;  
      Boolean IsCompliant;  
      Boolean IsDetected;  
      UInt32 MaxNoncomplianceCriticality;   
      String ModelName;  
      UInt32 ResourceID;  
      UInt32 SDMPackageVersion;   
      String UserName;  
};  
```  

## Methods  
 The `SMS_CI_ComplianceHistory` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `Uint32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 The unique ID of the configuration item. This ID is unique across sites.  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Version of the configuration item.  

 `ComplianceEndDate`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 The end date from which a Configuration Item was compliant, non-compliant or error. See corresponding start date in `ComplianceStartDate`.  

 `ComplianceStartDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The start date from which a Configuration Item was compliant, non-compliant or error. See corresponding end date in `ComplianceEndDate`.  

 `ComplianceValidationRuleFailures`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Number of validation rule failures.  

 `DesiredState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The resolved state in the context of Applications. Whether the Application was intended to be installed, uninstalled and so on.  

 `IsApplicable`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the configuration item is applicable on the computer.  

 `IsCompliant`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the configuration item is compliant on the computer.  

 `IsDetected`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the configuration item is detected on the computer.  

 `MaxNoncomplianceCriticality`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The maximum noncompliance severity reported by the client for the configuration item.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model Name of the configuration item.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The unique ID of the resource for the configuration item.  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 This property is deprecated. In System Center Configuration Manageronly the Configuration Item version is used.  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 User name.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application uses this class for compliance monitoring for a configuration item.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
