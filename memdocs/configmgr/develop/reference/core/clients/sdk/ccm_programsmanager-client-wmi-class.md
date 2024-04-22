---
title: CCM_ProgramsManager Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the CCM_ProgamsManager WMI class is a public client class that manages a specified software distribution program.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e31c3acb-6d31-43c9-a760-06d59c49e5b3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_ProgramsManager Client WMI Class
The `CCM_ProgamsManager` WMI class is a public client class, in Configuration Manager, that manages a specified software distribution program.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_ProgramsManager();  
```  

## Methods  
 The following table shows the methods in the `CCM_ProgamsManager` class.  

|Method|Description|  
|-|-|  
|[CancelDownload Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/canceldownload-method-in-class-ccm_programsmanager.md)|Cancels jobs that are downloading content that is required for legacy software distribution programs.|  
|[ExecuteProgram Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/executeprogram-method-in-class-ccm_programsmanager.md)|Manages the download of a legacy software distribution program.|  
|[ExecutePrograms Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/executeprograms-method-in-class-ccm_programsmanager.md)|Manages the download of a group of legacy software distribution programs.|  
|[PostponeProgramsToNonBusinessHours Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/postponeprogramstononbusinesshours-method-in-class-ccm_programsmanager.md)|Schedules legacy software distribution programs to run in the next available user-defined service window.|  

## Properties  
 The `CCM_ProgamsManager` class does not define any properties.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
