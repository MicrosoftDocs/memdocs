---
title: "SMS_ImagePackage Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 64961afc-3dca-4223-a626-80a80c3664b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ImagePackage Server WMI Class
The `SMS_ImagePackage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as the unit of distribution for image source files that are used to deploy a valid operating system, for example, Windows 10, in WIM format to a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImagePackage : SMS_PackageBaseclass  
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
      String ImageDiskLayout;  
      String ImageProperty;  
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
      String PackageID;  
      UInt32 PackageType;  
      UInt32 PkgFlags;  
      UInt32 PkgSourceFlag;  
      String PkgSourcePath;  
      String PreferredAddressType;  
      UInt32 Priority;  
      Boolean RefreshPkgSourceFlag;  
      SMS_ScheduleToken RefreshSchedule[];  
      String SecuredScopeNames[];  
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
 The following table shows the methods in `SMS_ImagePackage`.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_ImagePackage](../../../develop/reference/osd/addchangenotification-method-in-class-sms_imagepackage.md)|Adds an image package change notification.|  
|[AddDistributionPoints Method in Class SMS_ImagePackage](../../../develop/reference/osd/adddistributionpoints-method-in-class-sms_imagepackage.md)|Adds the distribution points for the package.|  
|[GetImageProperties Method in Class SMS_ImagePackage](../../../develop/reference/osd/getimageproperties-method-in-class-sms_imagepackage.md)|Reads all image properties from the specified WIM file to an XML string.|  
|[RefreshPkgSource Method in Class SMS_ImagePackage](../../../develop/reference/osd/refreshpkgsource-method-in-class-sms_imagepackage.md)|Refreshes the package source at all distribution points, when the package properties have not changed.|  
|[ReloadImageProperties Method in Class SMS_ImagePackage](../../../develop/reference/osd/reloadimageproperties-method-in-class-sms_imagepackage.md)|Reloads image properties from source WIM file and updates the database.|  
|[RunOfflineServicingManager Method in Class SMS_ImagePackage](../../../develop/reference/osd/runofflineservicingmanager-method-in-class-sms_imagepackage.md)|Triggers the offline servicing manager to run as soon as possible.|  
|[SetSourceSite Method in Class SMS_ImagePackage](../../../develop/reference/osd/setsourcesite-method-in-class-sms_imagepackage.md)|Sets the code of the source site for the image package.|  
|[Unlock Method in Class SMS_ImagePackage](../../../develop/reference/osd/unlock-method-in-class-sms_imagepackage.md)|Sets the source site to the current site, unlocking the image package.|  

## Properties  
 `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ExtendedData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ExtendedDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectDelay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectNumRetries`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IgnoreAddressSchedule`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ImageDiskLayout`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 An XML string of disk drive layout information about the source WIM image. The default value is "".  

 `ImageProperty`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 An XML string of image metadata for the source WIM file. The default value is "".  

 `ISVData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Language`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LastRefreshTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Manufacturer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFFilename`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFPublisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `NumOfPrograms`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageID`  
 Data type: `String`  

 Access type: [key]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 For this class, the package type is PKG_TYPE_IMAGE (257).  

 `PkgFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourceFlag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PreferredAddressType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshPkgSourceFlag`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: [max(15), lazy, ResID(725), ResDLL("SMS_RSTT.dll")]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ShareName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ShareType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

- Icon("Package.ico")  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  To get started using this class, see How to Add an Operating System Image Package in Configuration Manager.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
