---
title: CancelDownload method in class CCM_ProgramsManager
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 36538342-6f0d-4e64-84b8-aa56282c11c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CancelDownload Method in Class CCM_ProgramsManager
The `CancelDownload` WMI class method, in Configuration Manager, cancels jobs that are downloading content that is required for legacy software distribution programs.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 CancelDownload(  
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

 Identifier of the associated software distribution package.  

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
