---
description: Learn how to block specified client computers from communicating with the site in Configuration Manager using BlockClients.
title: BlockClients Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 72debf3d-bc74-4993-95b0-31cc99843d8e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# BlockClients Method in Class SMS_Collection
The `BlockClients` Windows Management Instrumentation (WMI) class method, in Configuration Manager, blocks specified client computers from communicating with the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 BlockClients(  
     UInt32 ResourceIDs[],  
     Boolean Blocked  
);  
```  

#### Parameters  
 `ResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of member resources.  

 `Blocked`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` if resources are blocked from communicating with the site. The default value is true.  

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
