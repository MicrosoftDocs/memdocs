---
title: "PostponeUpdatesToNonBusinessHours Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 466bbee1-f688-40f1-bfd2-ec819cfafa75
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# PostponeUpdatesToNonBusinessHours Method in Class CCM_SoftwareUpdatesManager
The `PostoneUpdatesToNonBusinessHours` WMI class method, in Configuration Manager, postpones a set of software updates to automatically install in non-business hours, which are specified by the user.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 PostponeUpdatesToNonBusinessHours(  
     [IN]  CCM_SoftwareUpdate CCMUpdates[],  
     [IN]  Boolean RebootImmediatelyAfterInstall  
);  
```  

#### Parameters  
 `CCMUpdates[]`  
 Data type: `CCM_SoftwareUpdate`  

 Qualifiers: [in]  

 Array of software updates to be installed.  

 `RebootImmediatelyAfterInstall`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if the computer restarts immediately after the installation; otherwise, `false`.  

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
