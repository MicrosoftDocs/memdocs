---
title: "InitializeData Method"
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
ms.assetid: a7c12a4e-85a0-4293-9888-095cc60640f5searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# InitializeData Method in Class SMS_ReplicationGroup
The `InitializeData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, reinitializes a specific replication group between two specified sites.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 InitializeData(  
     UInt32 ReplicationGroupID,  
     String SiteCode1,  
     String SiteCode2  
);  
```  

#### Parameters  
 `ReplicationGroupID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Unique identifier of the replication group.  

 `SiteCode1`  
 Data type: `String`  

 Qualifiers: [in]  

 Site code 1.  

 `SiteCode2`  
 Data type: `String`  

 Qualifiers: [in]  

 Site code 2.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ReplicationGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationgroup-server-wmi-class.md)
