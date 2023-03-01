---
description: Learn how to list instances of service windows in Configuration Manager using CCM_ServiceWindow class.
title: CCM_ServiceWindow Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6827bb41-2697-432a-bf41-0d5fd61f8565
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_ServiceWindow Client WMI Class
The `CCM_ServiceWindow` Client WMI class is a client class, in Configuration Manager, that lists instances of service windows.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_ServiceWindow  
{  
    UInt32 Duration;  
    Datetime EndTime;  
    String ID;   
    Datetime StartTime;  
    UInt32 Type;   
};  
```  

## Methods  
 The `CCM_ServiceWindow` class does not define any methods.  

## Properties  
 `Duration`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total duration, in seconds, of the service window.  

 `EndTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time to end the service window.  

 `ID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Service window identifier for this particular instance of service window.  

 `StartTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time to start the service window.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Type of service window. The following table shows the list of possible values.  

|Value|Service Window Type|Description|  
|-----------|-------------------------|-----------------|  
|1|ALLPROGRAM_SERVICEWINDOW|All Deployment Service Window|  
|2|PROGRAM_SERVICEWINDOW|Program Service Window|  
|3|REBOOTREQUIRED_SERVICEWINDOW|Reboot Required Service Window|  
|4|SOFTWAREUPDATE_SERVICEWINDOW|Software Update Service Window|  
|5|OSD_SERVICEWINDOW|Task Sequences Service Window|  
|6|USER_DEFINED_SERVICE_WINDOW|Corresponds to non-working hours|  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
