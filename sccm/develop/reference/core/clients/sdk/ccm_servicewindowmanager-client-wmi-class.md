---
title: "CCM_ServiceWindowManager Class"
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
ms.assetid: f8196309-a790-430c-88fb-d9f23be24a2dsearchScope: - ConfigMgr SDK
caps.latest.revision: 22
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_ServiceWindowManager Client WMI Class
The `CCM_ServiceWindowManager` WMI class is a client class, in Configuration Manager, manages service windows on the client computer.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_ServiceWindowManager();  
```  

## Methods  
 The following table shows the methods in the `CCM_ServiceWindowManager` class.  

|||  
|-|-|  
|**Method**|**Description**|  
|[GetCurrentWindowAvailableTime Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/getcurrentwindowavailabletime-method-in-class-ccm_servicewindowmanager.md)|Gets the time remaining in a currently-active service window for a specified type.|  
|[GetNextServiceWindowID Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/getnextservicewindowid-method-in-class-ccm_servicewindowmanager.md)|Gets the identifier of the next service window closest to the current time.|  
|[IsFutureWindowAvailable Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/isfuturewindowavailable-method-in-class-ccm_servicewindowmanager.md)|Determines whether a service window of a specified type and a given duration is going to be available.|  
|[IsWindowAvailableNow Method in Class CCM_SoftwareUpdatesManager](../../../../../develop/reference/core/clients/sdk/iswindowavailablenow-method-in-class-ccm_servicewindowmanager.md)|Determines whether a service window of a specified type and a given duration is available to run at the point of time when the call is made.|  

## Properties  
 The `CCM_ServiceWindowManager` class does not define any properties.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
