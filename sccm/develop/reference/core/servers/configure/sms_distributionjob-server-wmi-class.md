---
title: "SMS_DistributionJob Class"
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
ms.assetid: 37b7da5f-7aa3-407b-a703-079818b8c536searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DistributionJob Server WMI Class
The `SMS_DistributionJob` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a distribution point job.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionJob : SMS_BaseClass  
{  
    UInt32 Action;  
    Datetime CreationTime;  
    UInt32 DPID;  
    UInt32 DynamicOrder;  
    UInt64 JobID;  
    Datetime LastUpdateTime;  
    String NALPath;  
    UInt32 PackageVersion;  
    String PkgID;  
    UInt32 RemainingSize;  
    UInt32 ReStartTime;  
    UInt32 RetryCount;;  
    Datetime StartTime;  
    UInt32 State;  
    UInt64 TotalSize;  
};  
```  

## Methods  
 The `SMS_DistributionJob` class does not define any methods.  

## Properties  
 `Action`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Current job action. Possible values are:  

|||  
|-|-|  
|1|DISTSRC_ACTION_UPDATE|  
|2|DISTSRC_ACTION_ADD|  
|5|DISTSRC_ACTION_CANCEL|  

 `CreationTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Job creation time.  

 `DPID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Distribution point identifier.  

 `DynamicOrder`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Dynamic order for the job.  

 `JobID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read, key]  

 Job identifier.  

 `LastUpdateTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last update time of the job.  

 `NALPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Distribution point NAL path.  

 `PackageVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package version.  

 `PkgID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package identifier.  

 `RemainingSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Remaining size of the distribution job.  

 `ReStartTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Job restart time.  

 `RetryCount`  
 Data type: `UIn32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Retry count.  

 `StartTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Job start time.  

 `State`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Current job state. Possible values are:  

 `TotalSize`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date of the last status update.  

|||  
|-|-|  
|0|DISTSRC_STATE_PENDING|  
|1|DISTSRC_STATE_READY|  
|2|DISTSRC_STATE_STARTED|  
|3|DISTSRC_STATE_INPROGRESS|  
|4|DISTSRC_STATE_PENDING_RESTART|  
|5|DISTSRC_STATE_COMPLETE|  
|6|DISTSRC_STATE_FAILED|  
|7|DISTSRC_STATE_CANCELLED|  
|8|DISTSRC_STATE_SUSPENDED|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
