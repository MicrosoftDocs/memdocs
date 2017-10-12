---
title: "SMSEvent Class"
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
ms.assetid: 255fe69c-c404-4d21-820a-df11b1eb3048searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMSEvent Class
The `SmsEvent` class represents a System Center Configuration Manager event on the client. The class implements the `ICcmEvent` interface.  

## Methods and Properties  

|Term|Description|  
|----------|-----------------|  
|[ICcmEvent::EventType Property](../../../../../develop/reference/core/servers/manage/iccmevent--eventtype-property.md)|Indicates the type of Windows Management Instrumentation (WMI) event that is being raised.|  
|[ICcmEvent::RawEvent Property](../../../../../develop/reference/core/servers/manage/iccmevent--rawevent-property.md)|Adds information to custom events.|  
|[ICcmEvent::SetProperty Method](../../../../../develop/reference/core/servers/manage/iccmevent--setproperty-method.md)|Sets an event property.|  
|[ICcmEvent::Submit Method](../../../../../develop/reference/core/servers/manage/iccmevent--submit-method.md)|Submits an event to WMI.|  
|[ICcmEvent::SubmitPending Method](../../../../../develop/reference/core/servers/manage/iccmevent--submitpending-method.md)|Submits an event to WMI in situations where the Configuration Manager Agent Host (CCMEXEC) service might not be running.|  

## Remarks  
 The `ProgID` for the automation object is Microsoft.SMS.Event and it is implemented as part of Smscore.dll. The Visual Basic reference for early binding is SMSCorLib. The early binding object name is `SMSEvent`.  

## Requirements  
 smscore.dll  

### Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Status and State Client APIs](../../../../../develop/reference/core/servers/manage/status-client-apis.md)
