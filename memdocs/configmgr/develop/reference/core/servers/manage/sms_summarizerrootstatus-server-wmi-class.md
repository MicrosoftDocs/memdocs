---
title: SMS_SummarizerRootStatus Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_SummarizerRootStatus Windows Management Instrumentation class is an SMS Provider server class that represents a summarizer for the overall health of the entire site hierarchy.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7b416c99-5c38-4257-ab39-2f4355eec4d9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SummarizerRootStatus Server WMI Class
The `SMS_SummarizerRootStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a summarizer for the overall health of the entire site hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SummarizerRootStatus : SMS_BaseClass  
{  
    UInt32 Status;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_SummarizerRootStatus`.  

|Method|Description|  
|------------|-----------------|  
|[GetTallyIntervals Method in Class SMS_SummarizerRootStatus](../../../../../develop/reference/core/servers/manage/gettallyintervals-method-in-class-sms_summarizerrootstatus.md)|Gets an array of tally intervals and the default interval.|  

## Properties  
 `Status`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Value indicating the overall health of the site hierarchy. Possible values are listed below. Determining the overall status for the site hierarchy is based on the status of the child sites.  

| Value | Properties |
| ----- | ---------- |
|GREEN(0)|OK. All the child sites reported a GREEN status.|  
|YELLOW(1)|Warning. One or more child sites reported a YELLOW status, but no RED status was reported by a child site.|  
|RED(2)|Critical. One or more of the child sites reported a RED status.|  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
