---
title: "SMS_PackageStatusDetailSummarizer Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 19da2fc0-621b-4f59-95df-9ef23b46474a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PackageStatusDetailSummarizer Server WMI Class
The `SMS_PackageStatusDetailSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists the distribution summary for a given package for a given site in a hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageStatusDetailSummarizer : SMS_BaseClass  
{  
      UInt32 Failed;  
      UInt32 Installed;  
      String Name;  
      String PackageID;  
      UInt32 Retrying;  
      String SiteCode;  
      String SiteName;  
      UInt32 SourceVersion;  
      DateTime SummaryDate;  
      UInt32 Targeted;  
};  
```  

## Methods  
 The `SMS_PackageStatusDetailSummarizer` class does not define any methods.  

## Properties  
 `Failed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points in the site that have exceeded the number of retries allowed during an installation or removal operation and that are currently in a state of installation-failed or retry-failed.  

 `Installed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points in the site that have successfully installed the current source version of the package.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name assigned to the package.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [ key, SizeLimit("8")]  

 ID assigned by Configuration Manager for the package.  

 `Retrying`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points in the site that have had at least one failure during an installation or removal operation but have not yet exceeded the number of retries allowed and are currently in a state of installation-retrying or removal-retrying.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 Site code for each site that has at least one distribution point specified for the package.  

 `SiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Friendly display name for the site.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Version of the package source files.  

 `SummaryDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC) when a change in package status for this site was most recently reported.  

 `Targeted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The total number of distribution points in the site that are targeted for the package.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
