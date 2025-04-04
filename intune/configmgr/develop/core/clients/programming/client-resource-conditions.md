---
description: Learn how to utilize Configuration Manager's ability to be aware of system resources state and act accordingly using the LaunchConditions class.
title: "Client Resource Conditions"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: a17b4116-4491-4775-9d80-dea6e071801d
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3


---
# Client Resource Conditions
In Configuration Manager SP1, the Configuration Manager client has added the ability to be aware of system resources state and act accordingly. The resources being monitored are power, network, and user idleness. This addition makes the Configuration Manager client a better citizen in terms of optimizing power utilization and not disturbing the end user experience as much as possible.  

## LaunchConditions  
 A new property called `LaunchConditions` has been added to the `CCM_Scheduler_ScheduledMessage` class. The property can be a combination of the below values.  

|Value|Meaning|Comment|  
|-----------|-------------|-------------|  
|0|No resource conditions.|This is the same behavior as versions of Configuration Manager prior to SP1.|  
|1|Fire only when the battery is at low or above state.|Definition of critical/low/high battery state is defined in the [Windows SYSTEM_POWER_STATUS structure](/windows/win32/api/winbase/ns-winbase-system_power_status).|  
|2|Fire only when the battery is at high or changing state.|Definition of critical/low/high battery state is defined in the [Windows SYSTEM_POWER_STATUS structure](/windows/win32/api/winbase/ns-winbase-system_power_status).|  
|4|Fire only when the computer is charging.|Definition of critical/low/high battery state is defined in the [Windows SYSTEM_POWER_STATUS structure](/windows/win32/api/winbase/ns-winbase-system_power_status).|  
|8|Fire only when the user is idle.|This check is only performed on desktop systems.|  
|16|Fire only when the network is connected.||  

> [!NOTE]
>  By default, the value of `LaunchConditions` is 1, meaning no scheduled tasks will be fired when the battery is at critical state.  
>   
>  Another new property called `DeadlineMinutes` was added to `CCM_Scheduler_ScheduledMessage` SP1. The default value of `DeadlineMinutes` is 4320 (3 days). After the `DeadlineMinutes` timeout, unless the computer is at critical power state, the pending schedules will be fired.  

 The site control file allows programmatic access to feature specific value monitoring/changes. The specific site control file items and default values are listed below.  

|Site Control File Item|Default Value|  
|----------------------------|-------------------|  
|Hardware Inventory Launch Conditions|10 = fire only when battery is high+ and user is idle.|  
|App Scan And Enforce Launch Conditions|10 = fire only when battery is high+ and user is idle.|  
|Scan And Evaluation Launch Conditions|26 = fire only when battery is high+ and user is idle and network is connected.|  
|DCM CI Assignment Evaluation Launch Conditions|10 = fire only when battery is high+ and user is idle.|  
|Software Inventory Launch Conditions|10 = fire only when battery is high+ and user is idle.|  

## See Also  
 [CCM_Scheduler_ScheduledMessage Client WMI Class](../../../../develop/reference/core/clients/client-classes/ccm_scheduler_scheduledmessage-client-wmi-class.md)
