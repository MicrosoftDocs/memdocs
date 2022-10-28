---
title: FindMachineSite Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the FindMachineSite Windows Management Instrumentation class method gets site code information for a specific resource.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 19cf942a-a1e8-44de-b280-a66effd481d5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# FindMachineSite Method in Class SMS_Collection
The `FindMachineSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets site code information for a specific resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 FindMachineSite(  
        uint32 ResourceID,   
        string SiteCode[]  
);  

```  

#### Parameters  
 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Configuration Manager supplied ID that uniquely identifies a client resource.  

 `SiteCode[]`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Site code of the site with which the resource is associated.  

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
