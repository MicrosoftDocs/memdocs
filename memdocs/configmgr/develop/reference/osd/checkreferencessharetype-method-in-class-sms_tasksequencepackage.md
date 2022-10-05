---
title: CheckReferencesShareType Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the CheckReferencesShareType WMI class method checks all referred packages for this task sequence and returns all packages that are not shared.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 25ae479d-c63e-4b45-a8e7-2de6ff4b3222
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CheckReferencesShareType Method in Class SMS_TaskSequencePackage
The `CheckReferencesShareType` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that checks all referred packages for this task sequence and returns all packages that are not shared.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 CheckReferencesShareType   
{  
    [IN]    String PackageID  
    [OUT]   Boolean CanRunFromDP  
    [OUT]   String PacakgeIds[]  
    [OUT]   String PackageNames[]  
};  
```  

## Parameters  
 `PackageID`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Task sequence package identifier.  

 `CanRunFromDP`  
 Data type: `Boolean`  

 Qualifiers: [id("1"), out]  

 `true` if the package can be run from the distribution point.  

 `PacakgeIds`  
 Data type: `String Array`  

 Qualifiers: [id("2"), out]  

 Package identifiers for all referred packages for this task sequence that are not shared.  

> [!NOTE]
>  The incorrect spelling of the variable "PacakgeIds" is hardcoded in WMI.  

 `PackageNames`  
 Data type: `String Array`  

 Qualifiers: [id("3"), out]  

 Package names for all referred packages for this task sequence that are not shared.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
