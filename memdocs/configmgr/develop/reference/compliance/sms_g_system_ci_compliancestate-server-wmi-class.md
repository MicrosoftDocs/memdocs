---
title: SMS_G_System_CI_ComplianceState Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_G_System_CI_ComplianceState Windows Management Instrumentation class is an SMS Provider server class that represents hardware inventory class objects for the compliance state of a configuration item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a2242e16-4556-4e51-b2d8-f56b3c1014f5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_CI_ComplianceState Server WMI Class
The `SMS_G_System_CI_ComplianceState` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents hardware inventory class objects for the compliance state of a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_CI_ComplianceState : SMS_G_System  
{  
      UInt32 CI_ID;  
      String CI_UniqueID;   
      UInt32 CIVersion;  
      UInt32 ComplianceState;  
      String ComplianceStateName;  
      UInt32 DesiredState;  
      UInt32 IsApplicable;  
      UInt32 IsDetected;  
      UInt32 LastComplianceErrorID;  
      String LocalizedDisplayName;   
      UInt32 MaxNoncomplianceCriticality;  
      UInt32 ResourceID;  
      UInt32 SDMPackageVersion;   
      UInt32 UserID;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_G_System_CI_ComplianceState` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `Uint32`  

 Access type: Read  

 Qualifiers: [key]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 The unique ID of the configuration item. This ID is unique across sites.  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Version of the configuration item.  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The compliance state of the computer for the specified configuration item.  

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

 `DesiredState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Desired state of the configuration item on the computer.  

 `IsApplicable`  
 Data type: `Uint32`  

 Access type: Read  

 Qualifiers: None  

 Value indicating if the configuration item is applicable to the computer.  

 `IsDetected`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Value indicating if the configuration item is detected on the computer.  

 `LastComplianceErrorID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 ID of the last compliance status error.  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Localized display name for the compliance state.  

 `MaxNoncomplianceCriticality`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 The maximum noncompliance severity reported by the client for the configuration item.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_g_system_system-server-wmi-class.md).  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Version of the System Definition Model (SDM) package that is associated with the configuration item.  

 `UserID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the user.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the user.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class to update and determine the compliance state of the configuration item in the server database.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_g_system_system-server-wmi-class.md)
