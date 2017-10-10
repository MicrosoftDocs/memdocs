---
title: "GetContentHash Method"
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
ms.assetid: b3b83197-97f0-4d92-8b99-5b9954a6c3d4searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetContentHash Method in Class SMS_TaskSequencePackage
The `GetContentHash` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the hash of specific System Center Configuration Manager content.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetContentHash(  
      UInt32 ContentID,  
      UInt32 HashAlgID,  
      String Hash  
);  
```  

#### Parameters  
 `ContentID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the content.  

 `HashAlgID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 HashAlgID ….  

 `Hash`  
 Data type: `String`  

 Qualifiers: [out]  

 The hash for the content.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)
