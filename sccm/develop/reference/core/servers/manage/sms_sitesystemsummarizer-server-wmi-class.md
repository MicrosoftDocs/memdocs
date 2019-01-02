---
title: "SMS_SiteSystemSummarizer Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fea44c9c-78e2-456e-863e-de8863894892
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SiteSystemSummarizer Server WMI Class
The `SMS_SiteSystemSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a site system summarizer. The site system summarizer reports physical system health data for each system and each system role in the Configuration Manager site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteSystemSummarizer : SMS_BaseClass  
{  
      UInt32 AvailabilityState;  
      SInt64 BytesFree;  
      SInt64 BytesTotal;  
      DateTime DownSince;  
      UInt32 ObjectType;  
      SInt32 PercentFree;  
      String Role;  
      String SiteCode;  
      String SiteObject;  
      String SiteSystem;  
      UInt32 Status;  
};  
```  

## Methods  
 The `SMS_SiteSystemSummarizer` class does not define any methods.  

## Properties  
 `AvailabilityState`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Availability state of the site system. The default value is 0.  

 `BytesFree`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: None  

 Amount of free, unused storage space, in kilobytes, for the storage object.  

 `BytesTotal`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: None  

 Maximum amount of storage space, in kilobytes, of the storage object. A negative value indicates that information is currently unavailable.  

 `DownSince`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 Date and time when the storage object was first found to be down (inaccessible). The storage object is considered down if the site server fails to connect to the storage object due to network problems, security problems, or other problems. The value is `null` if the storage object is accessible. The time zone is based on the time zone of the `SiteCode` property.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Type of object for which the status is being reported. Possible values are:  

|||  
|-|-|  
|0|NALPATH. A directory.|  
|1|SQL_DB. An SQL Server database.|  
|2|SQL_LOG. An SQL Server transaction log.|  

 `PercentFree`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: None  

 Percentage of free storage space available on the storage object.  

 `Role`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Configuration Manager role performed by the site system, for example:  

- Distribution point  

- SQL Server  

- Software metering server  

- Component server  

- Site server  

  `SiteCode`  
  Data type: `String`  

  Access type: Read  

  Qualifiers: [key]  

  Site code of Configuration Manager site.  

  `SiteObject`  
  Data type: `String`  

  Access type: Read  

  Qualifiers: [key]  

  Network abstraction layer (NAL) path to a storage object that is one of the following:  

- Directory that contains files  

- Name of the database  

- Transaction log  

  `SiteSystem`  
  Data type: `String`  

  Access type: Read  

  Qualifiers: [key]  

  Name of the computer containing the storage object.  

  `Status`  
  Data type: `UInt32`  

  Access type: Read  

  Qualifiers: None  

  Status value indicating the health of the component. Possible values are:  

|||  
|-|-|  
|GREEN(0)|OK. The storage objects are well below their thresholds.|  
|YELLOW(1)|Warning. The storage objects are approaching their thresholds.|  
|RED(2)|Critical. The storage objects have exceeded their thresholds.|  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  An instance of this class is created for every storage object used by Configuration Manager. Storage objects are defined by the `SiteObject` property.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Status Server WMI Classes](../../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)
