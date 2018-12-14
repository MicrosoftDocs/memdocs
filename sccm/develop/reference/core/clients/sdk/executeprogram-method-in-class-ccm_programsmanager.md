---
title: "ExecuteProgram Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fee7a3d5-59c1-4134-a2da-08957cd01625
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ExecuteProgram Method in Class CCM_ProgramsManager
The `ExecuteProgram` WMI class method, in Configuration Manager, manages the download of a legacy software distribution program.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 ExecuteProgram(  
     [IN]  String ProgramID,  
     [IN]  String PackageID  
);  
```  

#### Parameters  
 `ProgramID`  
 Data type: `String`  

 Qualifiers: [in]  

 Identifier of the software distribution program.  

 `PackageID`  
 Data type: `String`  

 Qualifiers: [in]  

 Identifier of the associated package.  

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
