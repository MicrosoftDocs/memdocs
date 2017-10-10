---
title: "CCM_SoftwareUpdatesManager Class"
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
ms.assetid: 21f63cf9-a39d-4e05-913b-65fca65b9e62searchScope: - ConfigMgr SDK
caps.latest.revision: 22
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_SoftwareUpdatesManager Client WMI Class
The `CCM_SoftwareUpdatesManager` WMI class is a client class, in Configuration Manager, that exposes methods to install, schedule and other actions on set of software updates.  

 This interface is equivalent to the ICCMUpdatesDeployment COM interface in the Configuration Manager 2007 SDK.  

> [!IMPORTANT]
>  The software update client side SDK will only return set of updates which are deployed to client from Configuration Manager site server, and are applicable, and are yet to be installed on the client.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_SoftwareUpdatesManager();  
```  

## Methods  
 The following table shows the methods in the `CCM_SoftwareUpdatesManager` class.  

|||  
|-|-|  
|**Method**|**Description**|  
|[CancelDownload Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/canceldownload-method-in-class-ccm_softwareupdatesmanager.md)|Cancels an in-progress download of software updates during a deployment.|  
|[GetAllUpdatesUserExperience Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/getallupdatesuserexperience-method-in-class-ccm_softwareupdatesmanager.md)|Gets the user experience mode that determines how software updates are displayed on a target computer.|  
|[InstallUpdates Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/installupdates-method-in-class-ccm_softwareupdatesmanager.md)|Installs the software updates.|  
|[PostponeUpdatesToNonBusinessHours Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/postponeupdatestononbusinesshours-method-in-class-ccm_softwareupdatesmanager.md)|Postpones a set of software updates to automatically install in non-business hours, which are specified by the user.|  
|[SetAllUpdatesUserExperience Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/setallupdatesuserexperience-method-in-class-ccm_softwareupdatesmanager.md)|Sets the user experience mode that determines how software updates are displayed on a target computer.|  

## Properties  
 The `CCM_SoftwareUpdatesManager` class does not define any properties.  

## Remarks  
 This class is equivalent to the `ICCMUpdatesDeployment` class in System Center Configuration Manager 2007 COM SDK.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
