---
title: "GetTSRelatedToDriverCategory Method"
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
ms.assetid: 2261bb91-979c-49e4-a243-733d2339988esearchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetTSRelatedToDriverCategory Method in Class SMS_TaskSequencePackage
The `GetTSRelatedToDriverCategory` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets task sequence packages related to the specified category.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetTSRelatedToDriverCategory   
{  
    [IN]    String CategoryUniqueId,  
    [OUT]   String PacakgeIds[]  
    [OUT]   String PackageNames[]  
};  
```  

## Parameters  
 `CategoryUniqueId`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Unique ID of the category instance. This ID is unique across sites. The string length can be up to 512 characters.  

 `PacakgeIds`  
 Data type: `String` Array  

 Qualifiers: [id("2"), out]  

 Package identifiers for packages related to the specified category.  

> [!NOTE]
>  The incorrect spelling of the variable "PacakgeIds" is hardcoded in WMI.  

 `PackageNames`  
 Data type: `String` Array  

 Qualifiers: [id("3"), out]  

 Package names for packages related to the specified category.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
