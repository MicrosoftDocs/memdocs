---
title: "ActivateHierarchy Method"
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
ms.assetid: 51a21352-8184-4f0f-9fe0-365608ab1433searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ActivateHierarchy Method in Class SMS_MigrationSiteMapping
The `ActivateHierarchy` Windows Management Instrumentation (WMI) class method, in Configuration Manager, activates the hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ActivateHierarchy (  
     String sourceSite,  
     String wmiAccount,  
     String sqlAccount,  
     String destinationSiteCode,  
     String scheduleToken  
);  
```  

#### Parameters  
 `sourceSite`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The source site FQDN, netBIOS name or IP address.  

 `wmiAccount`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 The account name to access the WMI provider on the source site.  

 `sqlAccount`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The account name to access SQL server on the source site.  

 `destinationSiteCode`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 The destination site’s site code. This should be the top site.  

 `scheduleToken`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The schedule for the data gathering job.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MigrationEntity Server WMI Class](../../../../develop/reference/core/migration/sms_migrationentity-server-wmi-class.md)   
 [Migration Server WMI Classes](../../../../develop/reference/core/migration/migration-server-wmi-classes.md)
