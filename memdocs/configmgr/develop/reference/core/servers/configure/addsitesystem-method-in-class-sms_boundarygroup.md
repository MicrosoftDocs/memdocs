---
title: AddSiteSystem method in class SMS_BoundaryGroup
titleSuffix: Configuration Manager
description: Learn how to add a site system to a boundary group in Configuration Manager using the AddSiteSystem class.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4a422493-79e2-4d5e-92bd-4252403de149
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddSiteSystem Method in Class SMS_BoundaryGroup
The `AddSiteSystem` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds a site system to this boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddSiteSystem(  
   String ServerNALPath[];  
   UInt32 Flags[]  
);  
```  

#### Parameters  
 `ServerNALPath`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Network abstraction layer (NAL) path to the site system.  

 `Flags`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 Identifies the network connection speed between the site system server and the connecting clients. Possible values are:  

|Value|Connection speed|  
|-|-|  
|0|Fast|  
|1|Slow|  

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
