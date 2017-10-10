---
title: "CCM_ProgramsManager Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: e31c3acb-6d31-43c9-a760-06d59c49e5b3searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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

|||  
|-|-|  
|**Method**|**Description**|  
|[CancelDownload Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/canceldownload-method-in-class-ccm_programsmanager.md)|Cancels jobs that are downloading content that is required for legacy software distribution programs.|  
|[ExecuteProgram Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/executeprogram-method-in-class-ccm_programsmanager.md)|Manages the download of a legacy software distribution program.|  
|[ExecutePrograms Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/executeprograms-method-in-class-ccm_programsmanager.md)|Manages the download of a group of legacy software distribution programs.|  
|[PostponeProgramsToNonBusinessHours Method in Class CCM_ProgramsManager](../../../../../develop/reference/core/clients/sdk/postponeprogramstononbusinesshours-method-in-class-ccm_programsmanager.md)|Schedules legacy software distribution programs to run in the next available user-defined service window.|  

## Properties  
 The `CCM_ProgamsManager` class does not define any properties.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
