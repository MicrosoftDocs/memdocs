---
title: "ApproveClients Method"
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
ms.assetid: b6ebe9e7-0e31-4b88-a157-dd1b2fa3da1bsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ApproveClients Method in Class SMS_Collection
The `ApproveClients` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, approves specified client computers to join the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ApproveClients(  
     UInt32 ResourceIDs[],  
     Boolean Approved  
);  
```  

#### Parameters  
 `ResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of member resources.  

 `Approved`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` if resources are approved for the site. The default value is true.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
