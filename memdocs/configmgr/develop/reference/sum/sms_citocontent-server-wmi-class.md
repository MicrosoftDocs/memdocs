---
title: SMS_CIToContent Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that exposes the configuration item to content relationship for a software update.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: db224f8c-813e-455a-b280-70896c1e278e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CIToContent Server WMI Class
The `SMS_CIToContent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that exposes the configuration item to content relationship for a software update. It lists all the contents in the configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIToContent : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    String ContentDescription;  
    Boolean ContentDownloaded;  
    String ContentHash;  
    SInt32 ContentHashVersion;  
    SInt32 ContentID;  
    String ContentLocales[];  
    String ContentUniqueID;  
    SInt32 ContentVersion;  
    String ModelName;  
    UInt32 ObjectTypeID;  
    String SDMMethodType;  
    String SecuredModelName;  
};  
```  

## Methods  
 The `SMS_CIToContent` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, Not_null]  

 Unique ID of the configuration item corresponding to the update. This ID is unique only for the site. The ID is defined by the `CI_ID` property of [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ContentDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the update content.  

 `ContentDownloaded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 `true` if the content is downloaded; otherwise, `false`.  

 `ContentHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Hash of the content files.  

 `ContentHashVersion`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The content hash version.  

 `ContentID`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, Not_null]  

 ID for the software update content.  

 `ContentLocales`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 Array of locales associated with the content.  

 `ContentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 Unique ID of the content.  

 `ContentVersion`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 Version of the content.  

 `ModelName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, Not_null]  

 See [SMS_ObjectContentInfo Server WMI Class](../../../develop/reference/core/servers/console/sms_objectcontentinfo-server-wmi-class.md).  

 `SDMMethodType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, Not_null]  

 System Definition Model (SDM) method type corresponding to the configuration item.  

 `SecuredModelName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the secured model.

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is applicable to all types of configuration items, not just software updates. For a discussion of configuration item types, see the `CIType_ID` property of SMS_ConfigurationItemBaseClass Server WMI Class.  

  Your application can query this class to get the list of contents and files associated with the software update configuration item. The class can also be used to get the list of configuration items that contain the specified content.  

  Software update content must be downloaded manually. To identify the contents to download, your application queries `SMS_CIToContent` and obtains the list of `ContentID` properties matching the specified locale criteria. With this list, the application can obtain the associated download URL and related properties for the content files from [SMS_CIContentFiles Server WMI Class](../../../develop/reference/sum/sms_cicontentfiles-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CIContentFiles Server WMI Class](../../../develop/reference/sum/sms_cicontentfiles-server-wmi-class.md)   
 [About software update deployments](../../sum/about-software-updates-deployments.md)
