---
title: FindResourceSite method in class SMS_Collection
titleSuffix: Configuration Manager
description: In Configuration Manager, the FindResourceSite WMI class method gets site code information for resources.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 79e82dd3-a3c1-434d-a5f8-60db7d3bc8db
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# FindResourceSite Method in Class SMS_Collection
The `FindResourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets site code information for resources.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 FindResourceSite(  
        boolean IncludeSubCollections = false,   
        string SiteCode[],  
        uint32 ResourceNumber[]  
);  

```  

#### Parameters  
 `IncludeSubCollections`  
 Data type: `Boolean`  

 Qualifiers: [in, optional, deprecated]  

 true if subcollections are also marked for evaluation. If this parameter is set to false, subcollections are not included. The value defaults to false, if not specified.  

 `SiteCode[]`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Site code of the site with which the resource is associated.  

 `ResourceNumber`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Configuration Manager supplied ID that uniquely identifies a client resource.  

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
