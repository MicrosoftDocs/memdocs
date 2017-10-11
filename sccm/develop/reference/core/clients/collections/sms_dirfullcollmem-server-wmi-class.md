---
title: "SMS_DirFullCollMem Class"
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
ms.assetid: 1203863b-8971-4ef9-b3a6-2f394b80b839searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DirFullCollMem Server WMI Class
The `SMS_DirFullCollMem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the full collection membership of directly assigned collections.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DirFullCollMem : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_DirFullCollMem` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated ID containing eight characters that identifies a collection.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique Configuration Manager-supplied ID for the resource.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
