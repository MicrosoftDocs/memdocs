---
title: "SMS_DPStatusSummary Class"
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
ms.assetid: b9e0b6e6-b853-4bdc-8c23-063255ddbbcbsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPStatusSummary Server WMI Class
The `SMS_DPStatusSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a summary of the distribution point status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPStatusSummary : SMS_BaseClass  
{  
    UInt32 DeploymentType;  
    String Description;  
    String Name;  
    UInt32 NumberErrors;  
    UInt32 NumberInProgress;  
    UInt32 NumberInstalled;  
    UInt32 NumberUnknown;  
    DateTime SummarizationTime;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_DPStatusSummary` class.  

|Method|Description|  
|------------|-----------------|  
|[UpdateSummaryData Method in Class SMS_DPStatusSummary](../../../develop/reference/misc/updatesummarydata-method-in-class-sms_dpstatussummary.md)|Updates the summary data.|  

## Properties  
 `DeploymentType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Deployment type for distribution point status summary.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the distribution point status summary.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name.   

 `NumberErrors`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the failed distribution points.  

 `NumberInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the number of distribution point in progress.  

 `NumberInstalled`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the number of successfully installed distribution points.  

 `NumberUnknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the number of unknown distribution points.  

 `SummarizationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last update time.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
