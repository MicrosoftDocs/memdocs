---
title: "SMS_CI_CurrentComplianceStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d36889ae-8c02-441e-996d-64f98c970eae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CI_CurrentComplianceStatus Server WMI Class
The `SMS_CI_CurrentComplianceStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the compliance status for a baseline configuration item.  

## Syntax  

```  
Class SMS_CI_CurrentComplianceStatus : SMS_BaseClass  
{  
      UInt32 CI_ID;  
      String CI_UniqueID;  
      UInt32 CIVersion;   
      UInt32 ComplianceState;  
      String ComplianceStateName;  
      String ComplianceStatusDetails;  
      UInt32 ComplianceValidationRuleFailures;  
      UInt32 DesiredState;   
      UInt32 EnforcementState;  
      String EnforcementStateName;  
      Boolean IsApplicable;  
      Boolean IsDetected;   
      DateTime LastComplianceMessageTime;   
      DateTime LastEnforcementMessageTime;  
      UInt32 MaxNoncomplianceCriticality;  
      String ModelName;   
      UInt32 ResourceID;  
      UInt32 SDMPackageVersion;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_CI_CurrentComplianceStatus` class does not define any methods.  

## Properties  
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

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Version of the configuration item.  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The compliance state for the configuration item.  

 `ComplianceStateName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 The readable name of the compliance state. Possible values are:  

|Value|Compliance state|  
|-|-|  
|0|Compliance State Unknown|  
|1|Compliant|  
|2|Non-Compliant|  
|4|Error|  

 `ComplianceStatusDetails`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [lazy]  

 The noncompliance detail report sent by the client in XML format.  

 `ComplianceValidationRuleFailures`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The number of validation rule failures.  

 `DesiredState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Desired compliance state of the configuration item on the computer.  

 `EnforcementState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The enforcement state. Possible values are:  

|Value|Enforcement state|  
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

 `EnforcementStateName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 The name of the enforcement state.  

 `IsApplicable`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the configuration item is applicable on the computer.  

 `IsDetected`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the configuration item is detected on the computer.  

 `LastComplianceMessageTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 Date and time of the last compliance state message.  

 `LastEnforcementMessageTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 Date and time of the last enforcement state message.  

 `MaxNoncomplianceCriticality`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The maximum non-compliance severity reported by the client for the configuration item.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model name of the configuration item.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The unique ID of the resource for the configuration item.  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 System Definition Model (SDM) content version of the configuration item.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the user.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class for compliance monitoring for a baseline configuration item.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
