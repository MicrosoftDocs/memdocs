---
title: "IsWindowAvailableNow Method"
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
ms.assetid: 37702798-5d54-4ea0-90c8-df8fc66a248dsearchScope: - ConfigMgr SDK
caps.latest.revision: 20
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IsWindowAvailableNow Method in Class CCM_ServiceWindowManager
The `IsWindowAvailableNow` WMI class method, in Configuration Manager, determines whether a service window of a specified type and the given duration is available to run at the point of time when the call is made.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 IsWindowAvailableNow(  
     [IN]  UInt32 ServiceWindowType,  
     [IN]  Boolean FallbackToAllProgramsWindow,  
     [IN]  UInt32 MaxRuntime,  
     [OUT] Boolean CanProgramRunNow  
);  
```  

#### Parameters  
 `ServiceWindowType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Type of service window. The following table lists possible values.  

|Value|Service Window Type|Description|  
|-----------|-------------------------|-----------------|  
|1|ALLPROGRAM_SERVICEWINDOW|All Programs Service Window|  
|2|PROGRAM_SERVICEWINDOW|Program Service Window|  
|3|REBOOTREQUIRED_SERVICEWINDOW|Reboot Required Service Window|  
|4|SOFTWAREUPDATE_SERVICEWINDOW|Software Update Service Window|  
|5|OSD_SERVICEWINDOW|OSD Service Window|  
|6|USER_DEFINED_SERVICE_WINDOW|Corresponds to non-working hours|  

 `FallbackToAllProgramsWindow`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true`, if the generic **All programs window** service window is to be used when a window specified in `FallbackToAllProgramsWindow` is not available; otherwise, `false`.  

 `MaxRuntime`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Maximum run time, in minutes, that a software update installation has to complete before the installation is no longer monitored by Configuration Manager. This setting is also used to determine whether there is enough time to install the update before the end of a maintenance window. The default setting is 60 minutes for service packs and 5 minutes for all other software update types. Values can range from 5 to 9999 minutes.  

> [!IMPORTANT]
>  Make sure that the maximum run time value is not set for more time than the configured maintenance window or the software update installation will not initiate.  

 `CanProgramRunNow`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if a service window of the specified type and the given duration is available to run at the point of time when the call is made; otherwise, `false`.  

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
 [CCM_ServicewindowManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_servicewindowmanager-client-wmi-class.md)
