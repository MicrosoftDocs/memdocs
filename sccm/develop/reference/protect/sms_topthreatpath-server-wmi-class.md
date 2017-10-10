---
title: "SMS_TopThreatPath Class"
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
ms.assetid: 6d0ee93a-d87a-4f84-b977-f7d33fc5c678searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TopThreatPath Server WMI Class
The `SMS_ThreatPath` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents summarizes the threats path found in 7 days per collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ThreatPath : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 DuplicateCount;  
    String Path;  
    UInt64 ResourceID;  
    UInt64 ThreatID;  
    String ThreatName;  
    UInt32 TotalCount;  
};  
```  

## Methods  
 The `SMS_ThreatPath` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier of the collection.  

 `DuplicateCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of members with a threat in that path.  

 `Path`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Path of the threat.  

 `ResourceID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the resource.  

 `ThreatID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier of the threat.  

 `ThreatName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the threat.  

 `TotalCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of members in the collection.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
