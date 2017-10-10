---
title: "RedistributeAutoUpgradeClientContent Method"
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
ms.assetid: a38e35de-5e02-4574-8f2a-4f526ded22c0searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# RedistributeAutoUpgradeClientContent Method in Class SMS_Site
The `RedistributeAutoUpgradeClientContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, redistributes auto-upgrade client content to the specified distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RedistributeAutoUpgradeClientContent(  
     String DPNALPath  
);  
```  

#### Parameters  
 `DPNALPath`  
 Data type: `String`  

 Qualifiers: [in]  

 Distribution point NAL path.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
