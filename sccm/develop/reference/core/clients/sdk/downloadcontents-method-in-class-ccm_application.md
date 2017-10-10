---
title: "DownloadContents Method"
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
ms.assetid: 3f054d62-d84c-4c08-80b2-4d8869a05c09searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# DownloadContents Method in Class CCM_Application
The `DownloadContents` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that downloads the content for an application.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 DownloadContents   
{  
    [IN]    String Id  
    [IN]    String Revision  
    [IN]    Boolean IsMachineTarget  
    [IN]    String Priority  
    [OUT]   String JobId  
};  
```  

## Parameters  
 `Id`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Application identifier.    

 `Revision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Revision.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `true` if the application targets a device.    

 `Priority`  
 Data type: `String`  

 Qualifiers: [id("3"), in, valuemap]  

 Priority. Possible values are:   

||  
|-|  
|Foreground|  
|High|  
|Normal|  
|Low|  

 `JobId`  
 Data type: `String`  

 Qualifiers: [id("4"), out]  

 Job identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
