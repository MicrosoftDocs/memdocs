---
title: SMS_DeviceSettingPackage Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a device setting package in the database.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 85557c6d-9b3a-4c1c-aff7-b45dee1edec9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DeviceSettingPackage Server WMI Class
The `SMS_DeviceSettingPackage` Windows Management Instrumentation (WMI) class is an SMS Provider server class that represents a device setting package in the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceSettingPackage : SMS_PackageBaseclass  
{  
      UInt32 ActionInProgress;  
      String AlternateContentProviders;  
      String Description;  
      String DeviceSettingItemUniqueIDs[];  
      String DeviceSettingPackageXML;  
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
      String PackageID;  
      UInt32 PackageSize;  
      UInt32 PackageType;  
      UInt32 PkgFlags;  
      UInt32 PkgSourceFlag;  
      String PkgSourcePath;  
      String PlatformType;  
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
 The following table shows the methods in `SMS_DeviceSettingPackage`.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/addchangenotification-method-in-class-sms_devicesettingpackage.md)|Adds a device setting package change notification.|  
|[AddDistributionPoints Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/adddistributionpoints-method-in-class-sms_devicesettingpackage.md)|Adds the distribution points for the device setting package.|  
|[RefreshPkgSource Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/refreshpkgsource-method-in-class-sms_devicesettingpackage.md)|Refreshes the package source at all distribution points, when the package properties have not changed.|  
|[SetSourceSite Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/setsourcesite-method-in-class-sms_devicesettingpackage.md)|Sets the code of the source site for the device setting package.|  
|[Unlock Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/unlock-method-in-class-sms_devicesettingpackage.md)|Sets the source site to the current site, unlocking the device setting package.|  

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

 Not used for this class.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `DeviceSettingItemUniqueIDs`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 GUIDs or unique IDs of the device settings contained in the package.  

 `DeviceSettingPackageXML`  
 Data type: `String`  

 Access type: Write-only  

 Qualifiers: None  

 User interface used to provide device setting package XML through this property. The default value is "".  

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

 `PackageSize`  
 Data type: `UInt32`  

 Access type: Read  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

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

 For this class, the flag setting is STORAGE_DIRECT (2).  

 `PkgSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PlatformType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of platform to which the device setting package applies. The default value is "".  

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

 Access type: [max(15), lazy]  

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

 Qualifiers: [read,]  

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

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Mobile device setting packages use programs, distribution points, and advertisements to collections to distribute their content.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)   
 [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)
