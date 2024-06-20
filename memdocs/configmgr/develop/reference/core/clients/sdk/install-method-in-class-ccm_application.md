---
description: Learn how to install an application using the Install Windows Management Instrumentation (WMI) class method.
title: Install Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8666bb0c-1969-4c88-92db-853ed3128412
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Install Method in Class CCM_Application
The `Install` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that installs an application.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 Install   
{  
    [IN]    String Id  
    [IN]    String Revision  
    [IN]    Boolean IsMachineTarget  
    [IN]    UInt32 EnforcePreference  
    [IN]    String Priority  
    [IN]    Boolean IsRebootIfNeeded  
    [OUT]   String JobId  
};  
```  

## Parameters  
 `Id`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Application identifier.    

 `Revision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Revision.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `true` if the application targets a device.      

 `EnforcePreference`  
 Data type: `UInt32`  

 Qualifiers: [id("3"), in, values]  

 Enforce preference. Possible values are:   

|Value|Enforce preference|  
|-|-|  
|0|Immediate|  
|1|NonBusinessHours|  
|2|AdminSchedule|  

 `Priority`  
 Data type: `String`  

 Qualifiers: [id("4"), in, valuemap]  

 Priority. Possible values are:   

|Value|
|-|  
|Foreground|  
|High|  
|Normal|  
|Low|  

 `IsRebootIfNeeded`  
 Data type: `Boolean`  

 Qualifiers: [id("5"), in]  

 `true` if a reboot is needed.    

 `JobId`  
 Data type: `String`  

 Qualifiers: [id("6"), out]  

 Job identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
