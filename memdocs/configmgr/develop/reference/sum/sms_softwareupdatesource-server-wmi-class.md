---
title: "SMS_SoftwareUpdateSource Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7f08b462-c04a-4fdd-bf3b-89461f7f32ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SoftwareUpdateSource Server WMI Class
The `SMS_SoftwareUpdateSource` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all software update sources available on the site, for use in synchronizing metadata during a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareUpdateSource : SMS_BaseClass  
{  
      String ApplicabilityCondition;  
      DateTime DateCreated;  
      DateTime DateModified;  
      Boolean IsExpired;  
      String PublicKeys;  
      String ScanMethod;  
      String ScanMethodParameters;  
      String ScannerToolPkgID;  
      UInt32 ScanType;  
      UInt32 SourceContentType;  
      String SourceSite;  
      String UpdateSourceDescription;  
      UInt32 UpdateSourceID;  
      String UpdateSourceName;  
      String UpdateSourceUniqueID;  
      String UpdateSourceVersion;  
      String UpdateType;  
};  
```  

## Methods  
 The `SMS_SoftwareUpdateSource` class does not define any methods.  

> [!NOTE]
>  The `ResendObjectToAllSites Method in Class SMS_SoftwareUpdateSource` has been deprecated in Configuration Manager.  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Condition that the client evaluates before evaluating a software update. If the condition does not exist, the update is not evaluated.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the update source was created.  

 `DateModified`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the update source was last modified.  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the update source is no longer active. The default value is `false`.  

 `PublicKeys`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Public keys with which all the associated binaries are signed.  

 `ScanMethod`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Scan method for the update source.  

 `ScanMethodParameters`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Scan method parameters.  

 `ScannerToolPkgID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 ID of the scanner tool package associated with the update source.  

 `ScanType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of scan to use for the source. Possible values are:  

- WSUS  

- Offline source  

  `SourceContentType`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: None  

  Type of content distributed by the update source.  

  `SourceSite`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [not_null]  

  Site code for the update source site.  

  `UpdateSourceDescription`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  Description of the update source.  

  `UpdateSourceID`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: [key, not_null]  

  The unique ID of the software update source. This ID is unique only for the site.  

  `UpdateSourceName`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [not_null]  

  Name of the update source.  

  `UpdateSourceUniqueID`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [not_null]  

  The unique ID for the update source. This ID is unique across sites.  

  `UpdateSourceVersion`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [not_null]  

  Version of the update source.  

  `UpdateType`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [not_null]  

  Type of the update source.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application uses this class to set or modify the source of a software update so that metadata is properly synchronized during update deployment. Currently, the supported sources for software updates are Windows Server Update Services (WSUS) and ITMU/Offline Catalog.  

 To use this class, the application creates an `SMS_SoftwareUpdateSource` object and sets the properties as required for the particular software update and the source.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
