---
title: "IsFutureWindowAvailable Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 83ae2265-47db-441d-986f-7e3869ef8d9e
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# IsFutureWindowAvailable Method in Class CCM_ServiceWindowManager
The `IsFutureWindowAvailable` WMI class method, in Configuration Manager, determines whether a service window of a specified type and the given duration is going to be available.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 IsFutureWindowAvailable(  
     [IN]  UInt32 ServiceWindowType,  
     [IN]  Boolean FallbackToAllProgramsWindow,  
     [IN]  UInt32 MaxRuntime,  
     [OUT] Boolean WillProgramRunInFuture  
);  
```  

#### Parameters  
 `ServiceWindowType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Type of service window. The following table lists the possible values.  

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

 `true` if the generic **All programs window** service window is to be used when a window specified in `ServiceWindowType` is not available; otherwise, `false`.  

 `MaxRuntime`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Maximum run time, in seconds, that a software update installation has to complete before the installation is no longer monitored by Configuration Manager. This setting is also used to determine whether there is enough time to install the update before the end of a maintenance window. The default setting is 60 minutes (3600 seconds) for service packs and 5 minutes (300 seconds) for all other software update types.  

> [!IMPORTANT]
>  Make sure that the maximum run time value is not set for more time than the configured maintenance window or the software update installation will not initiate.  

 `WillProgramRunInFuture`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the specified service window is going to be available; otherwise, `false`.  

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
