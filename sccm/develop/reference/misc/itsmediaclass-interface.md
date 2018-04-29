---
title: "ITsMediaClass Interface"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d2e2146c-8c64-40ab-8b6f-6b7d1dd571c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITsMediaClass Interface
The `ITsMediaClass` automation interface, in System Center Configuration Manager, enables the creation of task sequence media for operating system deployment. This interface inherits from `IDispatch`.  

## In This Section  

|Term|Definition|  
|----------|----------------|  
|[ITsMediaClass::Cancel Method](../../../develop/reference/misc/itsmediaclass--cancel-method.md)|Cancels task sequence media creation.|  
|[ITsMediaClass::ConnectionOptions Property](../../../develop/reference/misc/itsmediaclass--connectionoptions-property.md)|Contains a comma-delimited list of name=value pairs to use when establishing the Windows Management Instrumentation (WMI) connection to the SMS Provider.|  
|[ITsMediaClass::CreateBootMedia Method](../../../develop/reference/misc/itsmediaclass--createbootmedia-method.md)|Creates task sequence boot media that download policy from a management point and allow a user to run a task sequence for operating system deployment.|  
|[ITsMediaClass::CreateCaptureMedia Method](../../../develop/reference/misc/itsmediaclass--createcapturemedia-method.md)|Creates capture media that can be used to capture an operating system from a reference computer.|  
|[ITsMediaClass::CreateStandaloneMedia Method](../../../develop/reference/misc/itsmediaclass--createstandalonemedia-method.md)|Creates stand-alone media from which to run an operating system image deployment|  
|[ITsMediaClass::CurrentStep Property](../../../develop/reference/misc/itsmediaclass--currentstep-property.md)|Contains the current step in task sequence media creation.|  
|[ITsMediaClass::DistributionPoints Property](../../../develop/reference/misc/itsmediaclass--distributionpoints-property.md)|Contains a comma-delimited list of distribution points, most preferable first.|  
|[ITsMediaClass::ErrorDetail Property](../../../develop/reference/misc/itsmediaclass--errordetail-property.md)|Contains a buffer in which additional error information can be retrieved from task sequence media creation.|  
|[ITsMediaClass::ExitCode Property](../../../develop/reference/misc/itsmediaclass--exitcode-property.md)|Contains the exit code for task sequence media creation.|  
|[ITsMediaClass::MediaLabel Property](../../../develop/reference/misc/itsmediaclass--medialabel-property.md)|Contains a label to help identify the task sequence media during media creation.|  
|[ITsMediaClass::NumSteps Property](../../../develop/reference/misc/itsmediaclass--numsteps-property.md)|Contains the number of steps necessary for task sequence media creation.|  
|[ITsMediaClass::ProviderName Property](../../../develop/reference/misc/itsmediaclass--providername-property.md)|Contains the name of the SMS Provider to which to connect.|  
|[ITsMediaClass::SiteCode Property](../../../develop/reference/misc/itsmediaclass--sitecode-property.md)|Contains the site code for the site server (not necessarily the target site code).|  
|[ITsMediaClass::Status Property](../../../develop/reference/misc/itsmediaclass--status-property.md)|Contains the status for task sequence media creation.|  
|[ITsMediaClass::StepInfo Property](../../../develop/reference/misc/itsmediaclass--stepinfo-property.md)|Contains information about the steps required for task sequence media creation.|  
|[ITsMediaClass::StepProgress Property](../../../develop/reference/misc/itsmediaclass--stepprogress-property.md)|Contains a value indicating the progress of task sequence media creation.|  

## Remarks  
 The UUID for `ITsMediaClass` is EBA491FD-A947-4f99-9F60-D615F810CCDC.  

## See Also  
 [TsMediaClass Client COM Automation Class](../../../develop/reference/misc/tsmediaclass-client-com-automation-class.md)   
 [Operating System Deployment Task Sequencing](../../../develop/osd/operating-system-deployment-task-sequencing.md)
