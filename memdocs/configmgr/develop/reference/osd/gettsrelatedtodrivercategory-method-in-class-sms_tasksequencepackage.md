---
title: "GetTSRelatedToDriverCategory Method"
titleSuffix: "Configuration Manager"
description: "The GetTSRelatedToDriverCategory WMI class method gets task sequence packages related to the specified category."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2261bb91-979c-49e4-a243-733d2339988e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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
