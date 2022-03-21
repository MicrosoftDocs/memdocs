---
title: "SMS_SoftwareMeteringAgentConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 70e86f99-feca-4d53-9e81-526be5fc7b96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SoftwareMeteringAgentConfig Server WMI Class
The `SMS_SoftwareMeteringAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers retrieve data about the software that they use.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareMeteringAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String DataCollectionSchedule;  
    Boolean Enabled;  
    String LastUpdateTimeOfRules;  
    UInt32 MaximumUsageInstancesPerReport;  
    String MeterRuleIDList[];  
    UInt32 MRUAgeLimitInDays;  
    UInt32 MRURefreshInMinutes;  
    UInt32 ReportTimeout;  
};  
```  

## Methods  
 The `SMS_SoftwareMeteringAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Software Metering Agent ID is 8.  

 `DataCollectionSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule for data collection.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `LastUpdateTimeOfRules`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Last updated time of the metering rules. This is not currently used.  

 `MaximumUsageInstancesPerReport`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum number of usage instances which is sent from the client to the site server when collecting software usage data.  

 `MeterRuleIDList`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier list of metering rules. This is not currently used.  

 `MRUAgeLimitInDays`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The age limit of the mostly recently used applications maintained on the client. Records older than this age limit are removed.  

 `MRURefreshInMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 How often the mostly recently used applications list is refreshed. When the applications list is refreshed, the aged records are removed.  

 `ReportTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum time that the client messaging framework attempts to transmit the report if the destination endpoint is unreachable.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
