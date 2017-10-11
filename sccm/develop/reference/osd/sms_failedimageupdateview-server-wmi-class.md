---
title: "SMS_FailedImageUpdateView Class"
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
ms.assetid: 65a68dc4-f599-4e9e-b578-3600fc24a202searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_FailedImageUpdateView Server WMI Class
The `SMS_FailedImageUpdateView` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents failed software update information in offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_FailedImageUpdateView : SMS_BaseClass  
{  
    SInt32 FailedImageCount;  
    String Title;  
    SInt32 UpdateID;  
};  
```  

## Methods  
 The `SMS_FailedImageUpdateView` class does not define any methods.  

## Properties  
 `FailedImageCount`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Offline image count that failed to install this update.  

 `Title`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Software update display name.  

 `UpdateID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Software update local unique ID.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
