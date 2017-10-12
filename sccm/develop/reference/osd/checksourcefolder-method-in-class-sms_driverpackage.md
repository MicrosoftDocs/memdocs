---
title: "CheckSourceFolder Method"
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
ms.assetid: 6b72a1e3-42c3-4481-ab79-f1199d187a28searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CheckSourceFolder Method in Class SMS_DriverPackage
The `CheckSourceFolder` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that checks the state of an empty driver source folder.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 CheckSourceFolder   
{  
    [IN]    String SourceFolder  
    [OUT]   SInt32 Result  
};  
```  

## Parameters  
 `SourceFolder`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Source folder.  

 `Result`  
 Data type: `SInt32`  

 Qualifiers: [id("1"), out]  

 Results of check. Possible values are:  

|||  
|-|-|  
|0|No error.|  
|1|The folder is not in UNC format.|  
|2|Cannot read/write to the folder.|  
|4|The folder is not empty.|  
|8|The folder is already used by another driver package.|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
