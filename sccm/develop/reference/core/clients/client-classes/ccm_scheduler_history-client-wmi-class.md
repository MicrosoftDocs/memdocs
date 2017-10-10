---
title: "CCM_Scheduler_History Class"
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
ms.assetid: 19fb3c27-e46c-43c3-bdce-ded0d40911f2searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_Scheduler_History Client WMI Class
In System Center Configuration Manager, the `CCM_Scheduler_History` class is a client Windows Management Instrumentation (WMI) class that represents the history for a schedule.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Scheduler_History {  
      String  ScheduleID;  
      String  UserSID;  
      DateTime  FirstEvalTime;  
      DateTime  ActivationMessageSent;  
      Boolean  ActivationMessageSentIsGMT;  
      DateTime  ExpirationMessageSent;  
      Boolean  ExpirationMessageSentIsGMT;     
      DateTime  LastTriggerTime;  
      String  TriggerState;  
};  
```  

## Properties  
 `ScheduleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [Not_Null:ToInstance, Key]  

 ID of the schedule to which this history item refers.  

 `UserSID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [Not_Null:ToInstance, Key]  

 User owning the schedule.  

 `FirstEvalTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [Not_Null:ToInstance, Key]  

 Date and time when the schedule was first evaluated by the scheduler.  

 `ActivationMessageSent`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Last time the activation message was sent for the schedule.  

 `ActivationMessageSentIsGMT`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the time indicated by `ActivationMessageSent` is in Universal Coordinated Time (UTC).  

 `ExpirationMessageSent`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Last date and time when the expiration message was sent for the schedule.  

 `ExpirationMessageSentIsGMT`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the time indicated by `ExpirationMessageSent` is in Universal Coordinated Time (UTC).  

 `LastTriggerTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Last date and time when a trigger on the schedule fired. A NULL value indicates that a trigger has not yet fired on the schedule.  

 `TriggerState`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 State information that individual triggers can set and query.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Scheduling Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/scheduling-client-wmi-classes.md)
