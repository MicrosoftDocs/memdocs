---
title: "SMS_SystemConsoleUser Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 9b5f27fc-e2e4-4c4e-8b30-f84293b886besearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SystemConsoleUser Client WMI Class
The `SMS_SystemConsoleUser` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that defines usage data about users, based on the Windows security event log.  

> [!NOTE]
>  For this class to gather usable data, the Auditing of Logon/Logoff policy must be turned on for each computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SystemConsoleUser  
{  
      DateTime LastConsoleUse;  
      UInt32 NumberOfConsoleLogons;  
      String SystemConsoleUser;  
      UInt32 TotalUserConsoleMinutes;  
};  
```  

## Methods  
 The `SMS_SystemConsoleUser` class does not define any methods.  

## Properties  
 `LastConsoleUse`  
 Data type: `DateTime`  

 Access type: Read only  

 Qualifiers: None  

 The last date and time when the user logged off from the console.  

 `NumberOfConsoleLogons`  
 Data type: `UInt32`  

 Access type: Read only  

 Qualifiers: None  

 The total number of logons recorded in the system security event log for the specific user.  

 `SystemConsoleUser`  
 Data type: `String`  

 Access type: Read only  

 Qualifiers: [key]  

 The user name for the user logged on to the console.  

 `TotalUserConsoleMinutes`  
 Data type: `UInt32`  

 Access type: Read only  

 Qualifiers: None  

 The total number of console logon minutes recorded in the system security event log for the user.  

## Remarks  
 This class gathers information about a specific user from the system security event log by using logon and logoff events. When a logon event is found, the associated logon ID is used to search for a matching logoff event. If more than one logoff event is found for a specific logon, then the last logoff event is used to calculate the amount of time that the user was logged on. This is because it is possible to issue more than one logoff request before the system actually performs the logoff action. If a matching logoff event cannot be found, the next shutdown event or logon event is used in place of a logoff event. If none of these can be found, the latest entry in the security log is used.  

> [!NOTE]
>  Only interactive logons are acknowledged by this class.  

 Some security logs can roll over frequently, or they can extend for several years. The time polled for this class is limited to the last 90 days.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_BrowserHelperObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledExecutable Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)
