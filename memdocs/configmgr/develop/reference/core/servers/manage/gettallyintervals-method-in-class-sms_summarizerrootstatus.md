---
title: "GetTallyIntervals Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 80b464c3-8174-448c-bd0b-eaaa0554fa54
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetTallyIntervals Method in Class SMS_SummarizerRootStatus
The `GetTallyIntervals` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets an array of tally intervals and the default interval.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 GetTallyIntervals(  
   String SiteCode,  
    String ComponentName,  
    String TallyIntervals[],  
    String DefaultInterval  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 The site code of the site for which the status is reported.  

 `ComponentName`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 The name of the component.  

 `TallyIntervals`  
 Data type: `String` Array  

 Qualifiers: [out]  

 The tally intervals.  

 `DefaultInterval`  
 Data type: `String`  

 Qualifiers: [out]  

 The default interval.  

## Return Values  
 An `SInt32` data type.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SummarizerRootStatus Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizerrootstatus-server-wmi-class.md)
