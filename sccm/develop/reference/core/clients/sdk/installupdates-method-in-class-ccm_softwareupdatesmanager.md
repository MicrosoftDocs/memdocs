---
title: "InstallUpdates Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 32d00893-e70c-4dbf-b864-ed828b7d9487
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# InstallUpdates Method in Class CCM_SoftwareUpdatesManager
The `InstallUpdates` WMI class method, in Configuration Manager, installs software updates that have been deployed to the client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 InstallUpdates(  
     [IN]  CCM_SoftwareUpdate CCMUpdates[]  
);  
```  

#### Parameters  
 `CCMUpdates[]`  
 Data type: `CCM_SoftwareUpdate`  

 Qualifiers: [in]  

 Array of software updates that are installed.  

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
 [CCM_SoftwareUpdatesManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_softwareupdatesmanager-client-wmi-class.md)
