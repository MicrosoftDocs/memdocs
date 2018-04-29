---
title: "SMS_UpdateComplianceStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f7789fb5-fa96-4e88-8737-9adcb0498c4f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UpdateComplianceStatus Server WMI Class
The `SMS_UpdateComplianceStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents the client computer compliance status for software updates.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdateComplianceStatus : SMS_BaseClass  
{  
      String ArticleID;  
      String BulletinID;  
      UInt32 CI_ID;  
      UInt32 EnforcementSource;  
      UInt32 LastEnforcementMessageID;  
      String LastEnforcementMessageName;  
      DateTime LastEnforcementMessageTime;  
      UInt32 LastEnforcementStatusMsgID;  
      DateTime LastStatusChangeTime;  
      DateTime LastStatusCheckTime;  
      String LocalizedDescription;  
      String LocalizedDisplayName;  
      String LocalizedInformativeURL;  
      UInt32 MachineID;  
      UInt32 Status;  
      String UpdateLocales;  
};  
```  

## Methods  
 The `SMS_UpdateComplianceStatus` class does not define any methods.  

## Properties  
 `ArticleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Knowledge base article ID for the software update.  

 `BulletinID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Bulletin ID for security updates released by Microsoft.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The ID of the software update configuration item. This ID is not unique across sites.  

 `EnforcementSource`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Source of the compliance enforcement action. Possible values are:  

|||  
|-|-|  
|0|NONE|  
|1|SMS|  
|2|USER|  
|3|NAP|  

 `LastEnforcementMessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The ID of the last enforcement state message received.  

 `LastEnforcementMessageName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the last enforcement state message.  

 `LastEnforcementMessageTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time of the last enforcement state message.  

 `LastEnforcementStatusMsgID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The ID of the last enforcement status message received.  

 `LastStatusChangeTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The date and time of the last compliance status change.  

 `LastStatusCheckTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The date and time of the last compliance status check.  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized description of the configuration item.  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized display name of the configuration item.  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 URL for additional localized information about the configuration item.  

 `MachineID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The ID of the target computer.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 The status of the target computer.  Possible values are:  

|||  
|-|-|  
|0|Detection state unknown|  
|1|Update is not required|  
|2|Update is required|  
|3|Update is installed| 

 `UpdateLocales`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Update locales.   

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 See About Configuration Baselines and Configuration Items for a discussion of compliance.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)   
 [Configuration Manager Software Updates](../../../develop/sum/software-updates.md)
