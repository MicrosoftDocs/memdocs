---
title: SMS_StateSystemConfig Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_StateSystemConfig WMI class is an SMS Provider server class that specifies how client computers report state messages.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: bbaeaac6-7d53-4214-b616-c10720cdd6bb
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_StateSystemConfig Server WMI Class
The `SMS_StateSystemConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers report state messages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StateSystemConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 BulkSendInterval;  
    UInt32 BulkSendIntervalHigh;  
    UInt32 BulkSendIntervalLow;  
    String CacheCleanoutInterval;  
    UInt32 CacheMaxAge;  
};  
```  

## Methods  
 The `SMS_StateSystemConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The State System Config Agent ID is 16.  

 `BulkSendInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reporting cycle, in minutes, for state messages with normal priority.  

 `BulkSendIntervalHigh`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reporting cycle, in minutes, for state messages with high priority.  

 `BulkSendIntervalLow`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reporting cycle, in minutes, for state messages with low priority.  

 `CacheCleanoutInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

 `CacheMaxAge`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
