---
title: "SMS_CH_Settings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c801d253-b949-4b1f-8a08-455f70e04ada
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CH_Settings Server WMI Class
The `SMS_CH_Settings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client status settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CH_Settings : SMS_BaseClass  
{  
    String ADRetrievingSchedule;   
    UInt32 CleanUpInterval;  
    UInt32 DDRInactiveInterval;  
    UInt32 HWInactiveInterval;  
    Boolean NeedADLastLogonTime;   
    UInt32 PolicyInactiveInterval;  
    UInt32 SettingsID;  
    UInt32 StatusInactiveInterval;  
    UInt32 SWInactiveInterval;  
};  
```  

## Methods  
 The `SMS_CH_Settings` class does not define any methods.  

## Properties  
 `ADRetrievingSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule for how frequently the system retrieves information from Active Directory.  

 `CleanUpInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 History clean up interval.  

 `DDRInactiveInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Heartbeat discovery inactive interval.  

 `HWInactiveInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Hardware inventory inactive interval.  

 `NeedADLastLogonTime`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Last logged on time from Active Directory.  

 `PolicyInactiveInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Policy request inactive interval.  

 `SettingsID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Settings ID.  

 `StatusInactiveInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Status message inactive interval.  

 `SWInactiveInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Software inventory inactive interval.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Client Status Server WMI Classes](../../../../../develop/reference/core/clients/status/client-status-server-wmi-classes.md)
