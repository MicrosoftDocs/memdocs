---
title: "SMS_PackageStatusRootSummarizer Class"
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
ms.assetid: 7899997c-7846-44f5-882c-add161280dcasearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_PackageStatusRootSummarizer Server WMI Class
The `SMS_PackageStatusRootSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists the distribution summary for a given package for all sites in a hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageStatusRootSummarizer : SMS_BaseClass  
{  
      UInt32 Failed;  
      UInt32 Installed;  
      String Name;  
      String PackageID;  
      UInt32 Retrying;  
      UInt32 SourceCompressedSize;  
      DateTime SourceDate;  
      String SourceSite;  
      UInt32 SourceSize;  
      UInt32 SourceVersion;  
      UInt32 Targeted;  
};  
```  

## Methods  
 The `SMS_PackageStatusRootSummarizer` class does not define any methods.  

## Properties  
 `Failed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points for this package that have exceeded the number of retries allowed during an installation or removal operation and that are currently in a state of installation-failed or retry-failed.  

 `Installed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points that have successfully copied the current source version of the package. A distribution point is considered installed until an update, refresh, or removal operation is specified.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("64")]  

 Name of the package.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key,SizeLimit("8")]  

 Configuration Manager-assigned ID for the package.  

 `Retrying`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points for this package that have had at least one failure during an installation or removal operation but have not yet exceeded the number of retries allowed and are currently in a state of installation-retrying or removal-retrying.  

 `SourceCompressedSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Size, in kilobytes, of the compressed version of the package source files.  

 `SourceDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when this version of the source files was created.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 Site code of the site where the package originated.  

 `SourceSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Size, in kilobytes, of the package source files.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Current version of the package source files, as defined by the originating site.  

 `Targeted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total number of distribution points (including child sites) that are specified to have a copy of the package. A distribution point remains targeted until it is specified for removal.  

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
