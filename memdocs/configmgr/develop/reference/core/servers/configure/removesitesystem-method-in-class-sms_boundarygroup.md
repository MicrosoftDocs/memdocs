---
title: RemoveSiteSystem method in class SMS_BoundaryGroup
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that removes site systems from a boundary group.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 82637714-bd3a-43a4-8584-cc443e0e8c09
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RemoveSiteSystem Method in Class SMS_BoundaryGroup
The `RemoveSiteSystem` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes site systems from this boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RemoveSiteSystem(  
   String ServerNALPath[]  
);  
```  

#### Parameters  
 `ServerNALPath`  
 Data type: `String` Array  

 Qualifiers: [in]  

 NAL path to the server.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroup-server-wmi-class.md)
