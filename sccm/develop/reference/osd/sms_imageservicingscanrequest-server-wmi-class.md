---
title: "SMS_ImageServicingScanRequest Class"
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
ms.assetid: 56060aed-2ae2-49c9-9446-a9016b4ea964searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ImageServicingScanRequest Server WMI Class
The `SMS_ImageServicingScanRequest` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents scan request for offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageServicingScanRequest : SMS_BaseClass  
{  
    String ImagePackageID;  
    DateTime LastRunDateTime;  
    SInt32 Status;  
};  
```  

## Methods  
 The `SMS_ImageServicingScanRequest` class does not define any methods.  

## Properties  
 `ImagePackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for offline servicing image that is installed on client computer.  

 `LastRunDateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last run time for this offline image.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Status for this offline image installation  

|||  
|-|-|  
|1|Success|  
|2|Failed|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
