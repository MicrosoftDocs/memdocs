---
title: SMS_TopThreatSummary Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that summarizes the top threats per collection.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8803e2a7-f4f2-4748-acc2-bcaeb777be7d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TopThreatSummary Server WMI Class
The `SMS_TopThreatSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that summarizes the top threats per collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TopThreatSummary : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 CollectionMembers;  
    String CollectionName;  
    UInt32 FailedCount;  
    DateTime FirstDetectionTime;  
    UInt32 InfectedCount;  
    Boolean IsAllowed;  
    Boolean IsExcluded;  
    Boolean IsRestored;  
    DateTime LastDetectionTime;  
    DateTime LastUpdateTime;  
    UInt32 PendingCount;  
    UInt32 RemediatedCount;  
    UInt32 Severity;  
    UInt32 ThreatCategoryID;  
    UInt64 ThreatID;  
    String ThreatName;  
};  
```  

## Methods  
 The `SMS_TopThreatSummary` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the collection.  

 `CollectionMembers`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of collection members.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the collection.  

 `FailedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Failed action client count.  

 `FirstDetectionTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 First time the malware is detected.  

 `InfectedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Infected client count.  

 `IsAllowed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if we've trigger the action to allow this malware in this collection.  

 `IsExcluded`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if we've chosen to exclude this malware path (in the scan list) in this collection.  

 `IsRestored`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if we've tried to restore this malware in this collection.  

 `LastDetectionTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last detection time.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last update time.  

 `PendingCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients with pending actions to finish the remediation of the malware in this collection.  

 `RemediatedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients where malware was remediated successfully in the collection.  

 `Severity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Threat severity. Possible values are:  

| Value | Threat severity |  
| ----- | --------------- |  
|0|Not Yet Classified|  
|1|Low|  
|2|Medium|  
|3|Not Used|  
|4|High|  
|5|Severe|  

 `ThreatCategoryID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Category identifier of the threat.  

 `ThreatID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the threat.  

 `ThreatName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the threat.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
