---
description: Learn how to use the SMS_SummarizerSiteStatus class to represent summarizer for the overall health of each site.
title: SMS_SummarizerSiteStatus Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7254b814-8959-4c26-96ab-05e175a534e0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SummarizerSiteStatus Server WMI Class
The `SMS_SummarizerSiteStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a summarizer for the overall health of each site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SummarizerSiteStatus : SMS_BaseClass  
{  
     String SiteCode;  
    UInt32 Status;  
};  
```  

## Methods  
 The `SMS_SummarizerSiteStatus` class does not define any methods.  

## Properties  
 `SiteCode`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Site code of the Configuration Manager site.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Value indicating the overall health of the site. Possible values are listed below. Determining the overall status for the site hierarchy is based on the status of Configuration Manager components and storage objects.  

| Value | Status |
| ----- | ------ |
|GREEN(0)|OK. There are no warning or error messages.|  
|YELLOW(1)|Warning. Warning messages were generated, but error messages were not generated. This status also indicates that the storage objects are approaching their threshold.|  
|RED(2)|Critical. There are error messages, or the storage objects have exceeded their thresholds.|  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
