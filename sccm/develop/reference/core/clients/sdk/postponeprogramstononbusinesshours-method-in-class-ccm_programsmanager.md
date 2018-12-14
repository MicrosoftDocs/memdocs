---
title: "PostponeProgramsToNonBusinessHours Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 775da6e9-420e-44d7-abdf-2dfe2ab705f9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# PostponeProgramsToNonBusinessHours Method in Class CCM_ProgramsManager
The `PostponeProgramsToNonBusinessHours` WMI class method, in Configuration Manager, schedules legacy software distribution programs to run in the next available user defined service window.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 PostponeProgramsToNonBusinessHours(  
     [IN]  CCM_Program CCMPrograms[],  
     [IN]  Boolean RebootImmediatelyAfterInstall  
);  
```  

#### Parameters  
 `CCMPrograms []`  
 Data type: `CCM_Program`  

 Qualifiers: [in]  

 Array of software distribution programs to be postponed.  

 `RebootImmediatelyAfterInstall`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if the computer restarts immediately after the installation, otherwise, `false`.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or nonzero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [CCM_ProgramsManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_programsmanager-client-wmi-class.md)
