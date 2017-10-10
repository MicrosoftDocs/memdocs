---
title: "SMS_TaskSequence_ApplicationInfo Class"
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
ms.assetid: e0240fff-c3bf-4d5c-8f21-d36f1f528ce3searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_ApplicationInfo Server WMI Class
The `SMS_TaskSequence_ApplicationInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application information for the application that is installed by using a task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ApplicationInfo :    
{  
    String Description;  
    String DisplayName;  
    String Name;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ApplicationInfo` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for System Center Configuration Manager application.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Display name for System Center Configuration Manager application.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name for System Center Configuration Manager application.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
