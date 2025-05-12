---
description: Article detailing the use of SMS_SiteDetailSummarizer to provide per-site status of components and the system.
title: SMS_SiteDetailSummarizer Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6b3cce2b-4ba9-4598-ad5a-cb79fc7c1eda
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SiteDetailSummarizer Server WMI Class
The `SMS_SiteDetailSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides per-site status of components and the system. An instance of this class is created for each site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteDetailSummarizer : SMS_BaseClass  
{  
      UInt32 AvailabilityState;  
      UInt32 DatabaseFree;  
      UInt32 Errors;  
      UInt32 Infos;  
      String SiteCode;  
      String SiteName;  
      UInt32 Status;  
      String TallyInterval;  
      UInt32 TransFree;  
      String Version;  
      UInt32 Warnings;  
};  
```  

## Methods  
 The `SMS_SiteDetailSummarizer` class does not define any methods.  

## Properties  
 `AvailabilityState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Availability state of the site. The default value is 0.  

 `DatabaseFree`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Percentage of free storage space available for the site databases.  

 `Errors`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Total number of error status messages reported by all server components in this site during the tally interval.  

 `Infos`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Total number of informational status messages reported by all server components in this site during the tally interval.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, SizeLimit("3")]  

 Site code of a Configuration Manager site.  

 `SiteName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Friendly name of the site.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [ToInstance]  

 Status value indicating the health of the component. Possible values are:  

| Value | Status |
| ----- | ------ |
|GREEN(0)|OK. There are no warning or error messages.|  
|YELLOW(1)|Warning. Warning messages were generated, but error messages were not generated.|  
|RED(2)|Critical. There are error messages.|  

 `TallyInterval`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Interval for which the detailed statistics apply. You must specify a tally interval in your WHERE clause to query instances of this class. The statistics are reset to zero each time the schedule elapses. To use this property, see How To Read Tally Intervals.  

 `TransFree`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Percentage of free storage space available for the transaction logs of the site databases.  

 `Version`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Version of Configuration Manager that is installed on the site, including the service pack if one is installed.  

 `Warnings`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Total number of warning status messages reported by all server components in this site during the tally interval.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class summarizes all informational, warning, and error messages for the site. An instance of the class is created for each server component that is running in the site.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
