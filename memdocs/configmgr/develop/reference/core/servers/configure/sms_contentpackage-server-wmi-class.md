---
title: "SMS_ContentPackage Class"
titleSuffix: "Configuration Manager"
description: "An SMS Provider server class that represents the content package."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f338598f-826c-4303-927f-9b007e1d2aac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ContentPackage Server WMI Class
The `SMS_ContentPackage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the content package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ContentPackage : SMS_PackageBaseclass  
{  
    UInt32 ActionInProgress;  
    String AlternateContentProviders;  
    String Description;  
    UInt8 ExtendedData[];  
    UInt32 ExtendedDataSize;  
    UInt32 ForcedDisconnectDelay;  
    Boolean ForcedDisconnectEnabled;  
    UInt32 ForcedDisconnectNumRetries;  
    UInt8 Icon[];  
    UInt32 IconSize;  
    Boolean IgnoreAddressSchedule;  
    UInt8 ISVData[];  
    UInt32 ISVDataSize;  
    String Language;  
    DateTime LastRefreshTime;  
    String LocalizedCategoryInstanceNames[];  
    String Manufacturer;  
    String MIFFilename;  
    String MIFName;  
    String MIFPublisher;  
    String MIFVersion;  
    String Name;  
    UInt32 NumOfPrograms;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    UInt32 PackageSize;  
    UInt32 PackageType;  
    UInt32 PkgFlags;  
    UInt32 PkgSourceFlag;  
    String PkgSourcePath;  
    String PreferredAddressType;  
    UInt32 Priority;  
    Boolean RefreshPkgSourceFlag;  
    SMS_ScheduleToken RefreshSchedule[];  
    String SecuredScopeNames[];  
    String SecurityKey;  
    String SedoObjectVersion;  
    String ShareName;  
    UInt32 ShareType;  
    DateTime SourceDate;  
    String SourceSite;  
    UInt32 SourceVersion;  
    String StoredPkgPath;  
    UInt32 StoredPkgVersion;  
    String Version;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ContentPackage` class.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/addchangenotification-method-in-class-sms_contentpackage.md)|Adds a package change notification.|  
|[AddContent Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/addcontent-method-in-class-sms_contentpackage.md)|Adds a set of contents to this content package|  
|[AddDistributionPointGroup Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/adddistributionpointgroup-method-in-class-sms_contentpackage.md)|Adds a distribution point group for the content package.|  
|[AddDistributionPoints Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/adddistributionpoints-method-in-class-sms_contentpackage.md)|Adds the distribution points for the content package.|  
|[Commit Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/commit-method-in-class-sms_contentpackage.md)|Called when all the contents have been added to the content package to start package processing.|  
|[RemoveContent Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/removecontent-method-in-class-sms_contentpackage.md)|Removes the content for the given ContentID from the package.|  
|[RefreshPkgSource Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/refreshpkgsource-method-in-class-sms_contentpackage.md)|Causes a refresh of the package source.|  
|[Unlock Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/unlock-method-in-class-sms_contentpackage.md)|Sets the source site to the current site, unlocking the package. **Important:**  This method is obsolete.|  
|[SetSourceSite Method in Class SMS_ContentPackage](../../../../../develop/reference/core/servers/configure/setsourcesite-method-in-class-sms_contentpackage.md)|Sets the code of the source site for the package.|  

## Properties  
 `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy, resdll, resid]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ExtendedData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ExtendedDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectDelay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectNumRetries`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IgnoreAddressSchedule`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ISVData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Language`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LastRefreshTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Manufacturer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFFilename`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFPublisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `NumOfPrograms`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The security type of the content.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageSize`  
 Data type: `UInt32`  

 Access type: Read  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourceFlag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PreferredAddressType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [stringenumeration]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshPkgSourceFlag`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: Read/Write  

 Qualifiers: [lazy, max]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SecurityKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The security key of the content. Content may security by app or package.  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ShareName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ShareType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Specifies whether the package uses the common package share on the distribution point or a custom share.  

 `SourceDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
