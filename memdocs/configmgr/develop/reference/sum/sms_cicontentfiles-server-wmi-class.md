---
title: SMS_CIContentFiles Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_CIContentFiles Windows Management Instrumentation class is an SMS Provider server class that lists all files associated with the content of a specific SMS_SoftwareUpdate Server WMI Class object.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a0a2dfbd-e3cf-439a-8607-31299f7c643f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CIContentFiles Server WMI Class
The `SMS_CIContentFiles` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all files associated with the content of a specific [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md) object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIContentFiles : SMS_BaseClass  
{  
    String CI_UniqueID;  
    UInt32 ContentID;  
    String FileHash;  
    String FileName;  
    SInt64 FileSize;  
    String FileVersion;  
    String ImportPath;  
    Boolean IsSigned;  
    UInt32 LanguageID;  
    String ModelName;  
    UInt32 ObjectTypeID;  
    String SourceURL;  
};  
```  

## Methods  
 The `SMS_CIContentFiles` class does not define any methods.  

## Properties  
 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ContentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, Not_null]  

 ID for the software update content. See the `ContentID` property of [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md).  

 `FileHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 The file hash.  

 `FileName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, Not_null]  

 File name, including the subdirectory path under the root directory.  

 `FileSize`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 The size of the file.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 The file version.  

 `ImportPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 The file location (including file name) relative to the import root.  

 `IsSigned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 `true` if the software update content is signed.  

 `LanguageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The language attribute of the file.  

 `ModelName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 Secured object class ID. Possible values are listed below.  

| ID value | Object type |  
| -------- | ----------- |  
|0|PKG_TYPE_REGULAR|  
|3|PKG_TYPE_DRIVER|  
|4|PKG_TYPE_TASK_SEQUENCE|  
|5|PKG_TYPE_SWUPDATES|  
|6|PKG_TYPE_DEVICE_SETTING|  
|8|PKG_CONTENT_PACKAGE|  
|257|PKG_TYPE_IMAGE|  
|258|PKG_TYPE_BOOTIMAGE|  
|259|PKG_TYPE_OSINSTALLIMAGE|  
|512|APPLICATION|  

 `SourceURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 URL where the source for the content file is located.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is used to determine update files to download for a particular update, for example, when there are different locales associated with the update. When using this class, first identify which contents need to be downloaded by querying [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md) and obtain the list of `ContentID` properties matching the specific language criteria. Given the list, you can then obtain the associated download URL and the related properties for the content files from `SMS_CIContentFiles`.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)   
 [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md)
