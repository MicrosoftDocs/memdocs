---
title: "SMS_PackageStatusDistPointsSummarizer Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9b365b0d-404c-4c37-a39a-3849c9d6d906
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_PackageStatusDistPointsSummarizer Server WMI Class
The `SMS_PackageStatusDistPointsSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists the distribution summary for packages on given site for a given distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageStatusDistPointsSummarizer : SMS_BaseClass  
{  
      DateTime LastCopied;  
      String PackageID;  
      UInt32 PackageType;  
      UInt32 SecuredTypeID;  
      String SecureObjectID;  
      String ServerNALPath;  
      String SiteCode;  
      String SourceNALPath;  
      UInt32 SourceVersion;  
      UInt32 State;  
      DateTime SummaryDate;  
};  
```  

## Methods  
 The `SMS_PackageStatusDistPointsSummarizer` class does not define any methods.  

## Properties  
 `LastCopied`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC), when the package source files were last successfully copied to the distribution point.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("8")]  

 Configuration Manager-assigned ID for the package.  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 The type of package.  

|Value|Description|  
|-----------|-----------------|  
|0|PKG_TYPE_REGULAR|  
|3|PKG_TYPE_DRIVER|  
|4|PKG_TYPE_TASK_SEQUENCE|  
|5|PKG_TYPE_SWUPDATES|  
|6|PKG_TYPE_DEVICE_SETTING|  
|7|PKG_TYPE_VIRTUAL_APP|  
|8|PKG_CONTENT_PACKAGE|  
|257|PKG_TYPE_IMAGE|  
|258|PKG_TYPE_BOOTIMAGE|  
|259|PKG_TYPE_OSINSTALLIMAGE|  

 `SecuredTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Secured type of related package.  

 `SecureObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Secure object ID. For app, it is model name. For others, it is package ID.  

 `ServerNALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Network abstraction layer (NAL) path to the distribution point.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 Site code of the site.  

 `SourceNALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 NAL path to the package source files.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Package source version number currently installed on this distribution point.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [ENUMERATION]  

 The state of the source files on the distribution point. Possible values are:  

|Value|State|  
|-|-|  
|0|INSTALLED|  
|1|INSTALL_PENDING|  
|2|INSTALL_RETRYING|  
|3|INSTALL_FAILED|  
|4|REMOVAL_PENDING|  
|5|REMOVAL_RETRYING|  
|6|REMOVAL_FAILED|  
|7|CONTENT_UPDATING|  
|8|CONTENT_MONITORING|  

 `SummaryDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC), when a change in package status for the sites was most recently reported.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
