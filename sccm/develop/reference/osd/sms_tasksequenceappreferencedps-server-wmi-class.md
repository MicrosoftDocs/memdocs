---
title: "SMS_TaskSequenceAppReferenceDps Class"
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
ms.assetid: 45bc90d3-77a5-4c99-bdc4-beffbd5c1929searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequenceAppReferenceDps Server WMI Class
The `SMS_TaskSequenceAppReferenceDps` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a distribution point to which a System Center Configuration Manager application in the task sequence is distributed.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequenceAppReferenceDps :    
{  
    String Hash;  
    String PackageID;  
    String ServerNALPath;  
    String SiteCode;  
    UInt32 SourceVersion;  
    String TaskSequenceID;  
};  
```  

## Methods  
 The `SMS_TaskSequenceAppReferenceDps` class does not define any methods.  

## Properties  
 `Hash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Hash for application.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Package ID for application.  

 `ServerNALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 NALPath for distribution point.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Site code for distribution point.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Source version for application.  

 `TaskSequenceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for task sequence package.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
