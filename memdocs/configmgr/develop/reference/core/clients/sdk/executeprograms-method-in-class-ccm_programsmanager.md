---
title: "ExecutePrograms Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0e3b8430-0571-4ae8-9e6f-e9e6a130adf1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ExecutePrograms Method in Class CCM_ProgramsManager
The `ExecutePrograms` WMI class method, in Configuration Manager, manages downloads of legacy software distribution programs.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 ExecutePrograms(  
     [IN]  CCM_Program CCMPrograms[],  
     [IN]  String SDKCallerId  
);  
```  

#### Parameters  
 `CCMPrograms[]`  
 Data type: `CCM_Program`  

 Qualifiers: [in]  

 Array of software distribution programs to download.  

 `SDKCallerId`  
 Data type: `String`  

 Qualifiers: [in]  

 Identifier of the caller.  

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
