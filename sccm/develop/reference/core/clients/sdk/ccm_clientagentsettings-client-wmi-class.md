---
title: "CCM_ClientAgentSettings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6388838c-8832-4e84-ba1a-bb66af8f79ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_ClientAgentSettings Client WMI Class
The `CCM_ClientAgentSettings` WMI class is a client class, in Configuration Manager, that contains common client agent settings.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_ClientAgentSettings  
{  
     String BrandingTitle;  
     UInt32 DayReminderInterval;  
     Boolean DisplayNewProgramNotification;  
     UInt32 EnableThirdPartyOrchestration;  
     UInt32 HourReminderInterval;  
     UInt32 InstallRestriction;  
     UInt32 ReminderInterval;  
     UInt32 SuspendBitLocker;  
     UInt32 SystemRestartTurnaroundTime;  
};  
```  

## Methods  
 The `CCM_ClientAgentSettings` class does not define any methods.  

## Properties  
 `BrandingTitle`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Title of the brand displayed in Configuration Manager. It maps to the client agent setting in Computer Agent, called **Organization name displayed in Software Center**  

 `DayReminderInterval`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Interval at which notifications are displayed to the user when there is required software pending and the earliest required deadline is less than 24 hours and greater than 1 hour.  

 `DisplayNewProgramNotification`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `false`, if no notifications are shown to the user for software availability or software installations. Only restart notifications are displayed. This property is mapped to the **Suppress notifications for new deployments** client agent setting in the Configuration Manager Admin Console.  

 `EnableThirdPartyOrchestration`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Flag to indicate whether Software Updates and Software Distribution agents wait for third-party components to install updates and applications.  

 `HourReminderInterval`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Interval at which notifications are displayed to the user when there is required software pending and the earliest required deadline is less than 1 hour.  

 `InstallRestriction`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Restriction flag to indicate who can initiate the installation. These options can be selected from the UI. The following table shows the list of possible values.  

|Value|Permission|  
|-----------|----------------|  
|0|Everyone|  
|1|Local administrators only|  
|2|Not used|  
|3|Local administrators and primary users|  
|4|No one|  

 `ReminderInterval`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Interval at which notifications are displayed to the user when there is required software pending and the earliest required deadline is greater than 24 hours.  

 `SuspendBitLocker`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Flag to indicate whether to suspend BitLocker Drive Protection PIN protectors for the restart initiated by Configuration Manager.  

 `SystemRestartTurnaroundTime`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Estimated turnaround time, in seconds, for a system restart.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
