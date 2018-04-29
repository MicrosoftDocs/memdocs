---
title: "SetSummarizationSettings Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9932385a-60a7-418a-828d-043869a04dfa
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SetSummarizationSettings Method in Class SMS_SummarizationSettings
In System Center Configuration Manager, the `SetSummarizationSettings` Windows Management Instrumentation (WMI) class method sets the summarization schedule.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
sint32 SetSummarizationSettings(  
     string SiteCode,   
     uint32 SummarizationType,   
     uint32 FirstIntervalMins,   
     uint32 SecondIntervalMins,   
     uint32 ThirdIntervalMins  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: `[in]`  

 The site code of the site associated with the summarization settings.  

 `SummarizationType`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Types of summarization. Possible values are:  

|||  
|-|-|  
|2|Application Deployment Summarization|  
|3|Application State Summarization (spans all previous and current deployments)|  

 `FirstIntervalMins`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 The interval in minutes between summarizations for deployments that have a start date within 30 days (for deployment summarizations) or applications that have been created in the last 30 days (for application state summarization).  

 `SecondIntervalMins`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 The interval in minutes between summarizations for deployments that have a start date within the last 30-90 days (for deployment summarizations) or applications that have been created within the last 30-90 days (for application state summarization).  

 `ThirdIntervalMins`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 The interval in minutes between summarizations for deployments that have a start date over 90 days (for deployment summarizations) or applications that have been created over 90 days ago (for application state summarization).  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SummarizationSettings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizationsettings-server-wmi-class.md)
