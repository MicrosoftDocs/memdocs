---
title: SMS_G_System_AdvancedThreatProtectionHealthStatus Class
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 677fcbd0-9b4d-4e44-8601-3975dc59c9b9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
description: An overview of SMS_G_System_AdvancedThreatProtectionHealthStatus Server WMI Class
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_AdvancedThreatProtectionHealthStatus Server WMI Class
The  `SMS_G_System_AdvancedThreatProtectionHealthStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Microsoft Defender for Endpoint client health status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_AdvancedThreatProtectionHealthStatus : SMS_G_System  
{  
    DateTime LastConnected;  
    UInt32 OnboardingState;  
    String OrgId;  
    UInt32 ResourceID;  
    Boolean SenseIsRunning;  
};          
```  

## Methods  
 The `SMS_G_System_AdvancedThreatProtectionHealthStatus` class does not define any methods.  

## Properties  
 `LastConnected`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: [not_null]  

 The time that the Microsoft Defender for Endpoint agent last connected to the cloud.  

 `OnboardingState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [not_null]  

 The onboarding state.  

 `OrgId`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [not_null]  

 The ID of the organization that the Microsoft Defender for Endpoint agent reports to.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 `SenseIsRunning`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: [not_null]  

 Indicates whether the Microsoft Defender for Endpoint agent is running.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
