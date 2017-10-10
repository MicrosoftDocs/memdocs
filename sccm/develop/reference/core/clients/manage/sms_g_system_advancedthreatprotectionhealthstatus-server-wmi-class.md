---
title: "SMS_G_System_AdvancedThreatProtectionHealthStatus Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 677fcbd0-9b4d-4e44-8601-3975dc59c9b9searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_G_System_AdvancedThreatProtectionHealthStatus Server WMI Class
The  `SMS_G_System_AdvancedThreatProtectionHealthStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Windows Defender Advanced Threat Protection (ATP) client health status.  

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

 The time that the Windows Defender ATP agent last connected to the cloud.  

 `OnboardingState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [not_null]  

 The onboarding state.  

 `OrgId`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [not_null]  

 The ID of the organization that the Windows Defender ATP agent reports to.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 `SenseIsRunning`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: [not_null]  

 Indicates whether the Windows Defender ATP agent is running.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Secured  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)
