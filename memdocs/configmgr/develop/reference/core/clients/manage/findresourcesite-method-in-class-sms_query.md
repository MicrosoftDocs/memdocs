---
description: Article describing how to use FindResourceSite in Configuration Manager to get site code information for resources from SQL.
title: FindResourceSite method in class SMS_Query
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 27d9cf32-728f-4834-97f3-4c9f28268fba
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# FindResourceSite Method in Class SMS_Query
The `FindResourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets site code information for resources from SQL.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 FindResourceSite(  
   Boolean IncludeSubCollections,  
   String SiteCode[],  
   UInt32 ResourceNumber[]  
);  
```  

#### Parameters  
 `IncludeSubCollections`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` if subcollections should be included. The default value is `false`.   

 `SiteCode`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Site code of the Configuration Manager site.   

 `ResourceNumber`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 The resource number.

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Query Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_query-server-wmi-class.md)
