---
description: Learn how the GetNextID Windows Management Instrumentation (WMI) class method, in Configuration Manager, retrieves the ID number that will be used for the next advertisement created.
title: GetNextID Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 54ce095c-443f-49e2-93d0-8ee3746608f1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetNextID Method in Class SMS_Advertisement
The `GetNextID` Windows Management Instrumentation (WMI) class method, in Configuration Manager, retrieves the ID number that will be used for the next advertisement created.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetNextID (  
    UInt32 NextID  
);  

```  

#### Parameters  
 `NextID`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 ID number for the next advertisement.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
