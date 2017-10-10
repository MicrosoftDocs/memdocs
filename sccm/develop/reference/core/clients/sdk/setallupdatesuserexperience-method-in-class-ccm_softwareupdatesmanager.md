---
title: "SetAllUpdatesUserExperience Method"
titleSuffix: "Configuration Manager"
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
ms.assetid: f9bddc84-7410-4c26-8448-e019ad5d4d5bsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SetAllUpdatesUserExperience Method in Class CCM_SoftwareUpdatesManager
The `SetAllUpdatesUserExperience` WMI class method, in Configuration Manager, sets the user experience mode that determines how software updates are displayed on a target computer.  

> [!NOTE]
>  This method can be used to hide or show all software updates in software center.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 SetAllUpdatesUserExperience(  
     [IN]  UInt32 UserExperience  
);  
```  

#### Parameters  
 `UserExperience`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The user experience flag. The following table shows the possible user experience mode values.  

|Value|User experience|  
|-----------|---------------------|  
|0|DEFAULT (per policy)|  
|1|INTERACTIVE|  
|2|QUIET|  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or nonzero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method is only available for local administrators. When a software update deployment has been prepared and software updates are available for installation, this method and the `GetAllUpdatesUserExperience` method can be used to configure the user experience.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [CCM_SoftwareUpdatesManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_softwareupdatesmanager-client-wmi-class.md)
