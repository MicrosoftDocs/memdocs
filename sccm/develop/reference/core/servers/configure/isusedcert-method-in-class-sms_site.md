---
title: "IsUsedCert Method"
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
ms.assetid: 8238a001-395e-4732-9042-bc9f33bcfe46searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IsUsedCert Method in Class SMS_Site
The `IsUsedCert` Windows Management Instrumentation (WMI) class method, in Configuration Manager, verifies whether the specified certificate is used.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean IsUsedCert(  
   String Certificate  
);  
```  

#### Parameters  
 `Certificate`  
 Data type: `String`  

 Qualifiers: [in]  

 The certificate to check against the site.  

## Return Values  
 `true` if the specified certificate is used on the site; otherwise `false`.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)   
 [GetClientInfo Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getclientinfo-method-in-class-sms_site.md)
