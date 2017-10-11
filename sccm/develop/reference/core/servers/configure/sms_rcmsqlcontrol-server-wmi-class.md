---
title: "SMS_RcmSqlControl Class"
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
ms.assetid: 10c827dc-7be9-443d-9e79-60a603a38b85searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_RcmSqlControl Server WMI Class
The `SMS_RcmSqlControl` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents ….  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_RcmSqlControl :    
{  
    SMS_RcmSqlControlProperty Props[];  
    String SiteCode;  
    String TypeName;  
};  
```  

## Methods  
 The `SMS_RcmSqlControl` class does not define any methods.  

## Properties  
 `Props`  
 Data type: `SMS_RcmSqlControlProperty` Array  

 Access type: Read/Write  

 Qualifiers: none  

 An array of `SMS_RcmSqlControlProperty` representing properties of the control.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 SiteCode.    

 `TypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 TypeName.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
