---
title: "SMS_AlertEmailTemplate Class"
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
ms.assetid: bd23b0f3-ca54-43f8-8c10-460166b9d339searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AlertEmailTemplate Server WMI Class
The `SMS_AlertEmailTemplate` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the email template embedded by `SMS_Subscription`.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AlertEmailTemplate    
{  
    UInt32 AlertID,  
    String Subject  
};  
```  

## Methods  
 The `SMS_AlertEmailTemplate` class does not define any methods.  

## Properties  
 `AlertID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier of the alert.  

 `Subject`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Subject of the email.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
