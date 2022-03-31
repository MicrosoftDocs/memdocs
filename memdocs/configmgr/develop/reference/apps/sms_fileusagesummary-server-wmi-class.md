---
title: "SMS_FileUsageSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8d8a7a1d-1ba4-4867-b1b5-042e186e5656
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: Learn about the simplified syntax, methods, properties and requirements of the SMS_FileUsageSummary server class.
---
# SMS_FileUsageSummary Server WMI Class
The `SMS_FileUsageSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides a usage summary of a metered file.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_FileUsageSummary : SMS_BaseClass  
{  
      UInt32 DistinctUserCount;  
      SInt64 FileID;  
      DateTime IntervalStart;  
      UInt32 IntervalWidth;  
      String SiteCode;  
};  
```  

## Methods  
 The `SMS_FileUsageSummary` class does not define any methods.  

## Properties  
 `DistinctUserCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Count of the distinct number of users who used the file during the summarization interval.  

 `FileID`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 File ID of the summarized file. To find the file information, match `FileID` with the ID in [SMS_ProductFileInfo Server WMI Class](../../../develop/reference/apps/sms_productfileinfo-server-wmi-class.md). To find the rules that caused the file to be metered, match `FileID` to the ID in [SMS_MeteredFiles Server WMI Class](../../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md).  

 `IntervalStart`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Start time of the summarization interval.  

 `IntervalWidth`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Size of the summarization interval, in minutes. Possible values are 15 and 60.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Site code for the clients that used the file during the summarization interval. This identifies the site that originally generated the summary.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class counts the number of distinct users and computers that used a metered file during a particular interval on a particular site.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
