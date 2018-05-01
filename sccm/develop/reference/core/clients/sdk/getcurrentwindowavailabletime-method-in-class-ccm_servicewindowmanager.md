---
title: "GetCurrentWindowAvailableTime Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f3492456-84e4-44e4-ae30-b0f0073c62ce
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetCurrentWindowAvailableTime Method in Class CCM_ServiceWindowManager
The `GetCurrentWindowAvailableTime` WMI class method, in Configuration Manager, gets the time remaining in a currently active service window for a specified type.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetCurrentWindowAvailableTime(  
     [IN]  UInt32 ServiceWindowType,  
     [IN]  Boolean FallbackToAllProgramsWindow,  
     [OUT] UInt32 WindowAvailableTime  
);  
```  

#### Parameters  
 `ServiceWindowType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Type of service window. The following table shows the list of possible values.  

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

 `WindowAvailableTime`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Available time remaining for service window.  

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
