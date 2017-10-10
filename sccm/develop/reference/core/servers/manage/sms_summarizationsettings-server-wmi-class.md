---
title: "SMS_SummarizationSettings Class"
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
ms.assetid: d826df70-49be-4272-a777-b9fa5f720c96searchScope: - ConfigMgr SDK
caps.latest.revision: 14
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SummarizationSettings Server WMI Class
The `SMS_SummarizationSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents the site summarization settings for a site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SummarizationSettings : SMS_BaseClass  
{  
    String ComponentName;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_SummarizationSettings` class.  

|Method|Description|  
|------------|-----------------|  
|[GetSummarizationSettings Method in Class SMS_SummarizationSettings](../../../../../develop/reference/core/servers/manage/getsummarizationsettings-method-in-class-sms_summarizationsettings.md)|Gets the summarization schedule.|  
|[SetSummarizationSettings Method in Class SMS_SummarizationSettings](../../../../../develop/reference/core/servers/manage/setsummarizationsettings-method-in-class-sms_summarizationsettings.md)|Sets the summarization schedule.|  

## Properties  
 `ComponentName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null, read]  

 Name of the Configuration Manager component.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Status Server WMI Classes](../../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)
