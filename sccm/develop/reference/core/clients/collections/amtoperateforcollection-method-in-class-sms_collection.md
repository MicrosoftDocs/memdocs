---
title: "AMTOperateForCollection Method"
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
ms.assetid: a3af06b4-8717-4d71-90e8-e0558fcb74a2searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# AMTOperateForCollection Method in Class SMS_Collection
The `AMTOperateForCollection` Windows Management Instrumentation (WMI) class method, in Configuration Manager, executes an Intel Active Management (AMT) operation on a collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AMTOperateForCollection(     
     UInt32 Opcode  
);  
```  

#### Parameters  
 `Opcode`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The AMT operation to execute. The following table provides the list of supported actions:  

|Value|Description|  
|-----------|-----------------|  
|1|WakeUp: Brings a sleeping computer back into the powered-on state.|  
|2|Restart: Causes a hard reset of the computer and the computer is then powered on. This does not shut the operating system down.|  
|3|Shutdown: Causes a hard reset of the computer. This does not shut the operating system down.|  
|8|DiscoveryBMC: Detects the AMT capability from an Out of Band service point. This populates the AMTStatus and AMTFullVersion properties of the corresponding SMS_R_System record.|  
|16|ReinventoryBMC: Currently unimplemented.|  
|8192|ClearAuditLog: Clears the audit log entries.|  

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
