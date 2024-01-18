---
title: GetClassesWithData Method
description: Learn how the GetClassesWithData Windows Management Instrumentation (WMI) class method gets the names of the classes that have inventory data for a resource.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 0e49fcbc-5ba9-4c6b-a88d-5eecdad31d50
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetClassesWithData Method in Class SMS_ResourceMap
The `GetClassesWithData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the names of the classes that have inventory data for a resource.  

## Syntax  

```  
SInt32 GetClassesWithData(  
     UInt32 ResourceId,  
     Boolean History,  
     String ClassNames[]  
);  
```  

#### Parameters  
 `ResourceId`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the resource.  

 `History`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 TRUE to include history.  

 `ClassNames`  
 Data type: `String`  

 Qualifiers: [out]  

 Names of classes that have inventory for the specified resource.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md)
