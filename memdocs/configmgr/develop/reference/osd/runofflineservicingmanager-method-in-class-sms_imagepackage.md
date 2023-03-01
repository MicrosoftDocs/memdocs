---
title: RunOfflineServicingManager Method in SMS_ImagePackage
titleSuffix: Configuration Manager
description: The RunOfflineServicingManager WMI class method updates the site control file of the offline servicing manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 95f79650-f052-4038-bd61-bd8554541b90
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RunOfflineServicingManager Method in Class SMS_ImagePackage
The `RunOfflineServicingManager` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that updates the site control file of the offline servicing manager to run the offline image servicing component as soon as possible on the specified operating system image at the specified site server.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 RunOfflineServicingManager   
{  
    [IN]    String SiteCode  
    [IN]    String ServerName  
    [IN]    String PackageID  
    [IN]    UInt32 PackageType  
};  
```  

## Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Site code of the site where offline servicing of the operating system image is requested.  

 `ServerName`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Name of the site server where offline servicing of the operating system is requested (server1.domain1.net).  

 `PackageID`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 The package identifier of the operating system image to be patched with software updates through offline servicing.  

 `PackageType`  
 Data type: `UInt32`  

 Qualifiers: [id("3"), in]  

 The package type of the operating system image or operating system upgrade package.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
