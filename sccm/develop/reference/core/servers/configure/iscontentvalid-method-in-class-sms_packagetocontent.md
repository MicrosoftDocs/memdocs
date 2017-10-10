---
title: "IsContentValid Method"
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
ms.assetid: 371c8d22-2384-4c28-8255-50e94e6fdf49searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IsContentValid Method in Class SMS_PackageToContent
The `IsContentValid` Windows Management (WMI) class method, in System Center Configuration Manager, determines if the package content is valid.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean IsContentValid();  
```  

#### Parameters  
 None.  

## Return Values  
 A `Boolean` data type that is `true` if the package contains all the files for the content; otherwise `false`.  

## Remarks  
 This method checks the package to ensure that all files are available for the content. It also checks to ensure that the licensing terms are met.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PackageToContent Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagetocontent-server-wmi-class.md)
