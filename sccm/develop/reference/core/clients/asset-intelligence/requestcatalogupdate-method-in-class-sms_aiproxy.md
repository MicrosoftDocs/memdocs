---
title: "RequestCatalogUpdate Method"
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
ms.assetid: cd764f0e-44bf-4719-9ce2-4aefafee0674searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# RequestCatalogUpdate Method in Class SMS_AIProxy
The `RequestCatalogUpdate` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, synchronizes the Asset Intelligence catalog with the System Center Online service.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RequestCatalogUpdate(      
     string ProxyName  
);  
```  

#### Parameters  
 `ProxyName`  
 Data type: `String`  

 Qualifiers: [in]  

 The `SMS_AIProxy` server name. This is located in the `ProxyName` property.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AIProxy Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aiproxy-server-wmi-class.md)
