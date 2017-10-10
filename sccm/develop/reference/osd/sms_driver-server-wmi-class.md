---
title: "SMS_Driver Class"
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
ms.assetid: e42884a1-a4db-432c-ad22-5c2474e8a102searchScope: - ConfigMgr SDK
caps.latest.revision: 20
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Driver Server WMI Class
The `SMS_Driver` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents device drivers, in the driver catalog, that can be installed as part of a task sequence in an operating system deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Driver : SMS_ConfigurationItemBaseClass  
{  
      String ApplicabilityCondition;  
      String CategoryInstance_UniqueIDs[];  
      UInt32 CI_ID;  
      String CI_UniqueID;  
      UInt32 CIType_ID;  
      UInt32 CIVersion;  
      UInt64 ConfigurationFlags;  
      String ContentSourcePath;  
      String CreatedBy;  
      DateTime DateCreated;  
      DateTime DateLastModified;  
      Boolean DriverBootCritical;  
      String DriverClass;  
      DateTime DriverDate;  
      String DriverINFFile;  
      String DriverProvider;  
      Boolean DriverSigned;  
      String DriverSigner;  
      String DriverType;  
      String DriverVersion;  
      DateTime EffectiveDate;  
      UInt32 EULAAccepted;  
      Boolean EULAExists;  
      DateTime EULASignoffDate;  
      String EULASignoffUser;  
      UInt32 ExecutionContext;  
      Boolean IsBundle;  
      Boolean IsDigest;  
      Boolean IsEnabled;  
      Boolean IsExpired;  
      Boolean IsHidden;  
      Boolean IsLatest;  
      Boolean IsQuarantined;  
      Boolean IsSuperseded;  
      Boolean IsUserDefined;  
      String LastModifiedBy;  
      String LocalizedCategoryInstanceNames[];  
      String LocalizedDescription;  
      String LocalizedDisplayName;  
      SMS_CI_LocalizedEulas LocalizedEulas[];  
      SMS_CI_LocalizedProperties LocalizedInformation[];  
      String LocalizedInformativeURL;  
      UInt32 LocalizedPropertyLocaleID;  
      UInt32 ModelID;  
      String ModelName;  
      UInt32 PermittedUses;  
      String PlatformCategoryInstance_UniqueIDs[];  
      UInt32 PlatformType;  
      SMS_SDMPackageLocalizedData SDMPackageLocalizedData[];  
      UInt32 SDMPackageVersion;  
      String SDMPackageXML;  
      String SecuredScopeNames[];  
      String SedoObjectVersion;  
      String SourceSite;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_Driver`.  

|Method|Description|  
|------------|-----------------|  
|[CreateFromINF Method in Class SMS_Driver](../../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md)|Creates an `SMS_Driver` object based on information from the specified source path and INF file.|  
|[CreateFromINFs Method in Class SMS_Driver](../../../develop/reference/osd/createfrominfs-method-in-class-sms_driver.md)|Creates `SMS_Driver` objects based on information from the specified source path and one or more INF files.|  
|[CreateFromOEM Method in Class SMS_Driver](../../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md)|Creates a set of `SMS_Driver` objects referenced by the specified Txtsetup.oem file.|  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("512"), not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `CategoryInstance_UniqueIDs`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:[unique, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 For this class, the type ID is Driver (6).  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ContentSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The location of the driver files. When a driver is added to a driver package or a boot image the SMS Provider copies files from this location. The path must be a Universal Naming Convention (UNC) path accessible by the SMS Provider, for example, \\\smsserver\drivers\microsoft\vmscsi, as the path for INF files.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `DateLastModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `DriverBootCritical`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the driver is boot-critical. A mass storage driver imported from a txtsetup.oem file that needs to be installed before booting into a pre-Windows Vista operating system.  

 `DriverClass`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The class of device that the driver supports (such as Net or Display) as reported by the driver's INF file.  

 `DriverDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the driver was written as reported by the INF file.  

 `DriverINFFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Relative path and file name of the driver INF file, relative to `ContentSourcePath`.  

 `DriverProvider`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the company or author of the driver file as reported in the INF file. This property does not necessarily reflect the device manufacturer.  

 `DriverSigned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the driver source file is digitally signed by a recognized authority. For example, the Windows Hardware Quality Lab.  

 `DriverSigner`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the digital signer if the driver source file is signed.  

 `DriverType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The type of driver. Currently the only valid value for this is INF.  

 `DriverVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Version number of the driver, as specified by the driver provider.  

 `EffectiveDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `EULAAccepted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `EULAExists`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `EULASignoffDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `EULASignoffUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `ExecutionContext`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsHidden`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsLatest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsQuarantined`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsSuperseded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LocalizedEulas`  
 Data type: `SMS_CI_LocalizedEulas Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Not used.  

 `LocalizedInformation`  
 Data type: `SMS_CI_LocalizedProperties Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Language-specific localized information about the driver:  

-   String  DisplayName  

-   String  Description  

-   String  InformativeURL  

-   UInt32  LocaleID  

 This property is used to change the display name and description for a driver that supports multiple languages.  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `ModelID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `PermittedUses`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `PlatformType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `PlatformCategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `SDMPackageLocalizedData`  
 Data type: `SMS_SDMPackageLocalizedData` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `SDMPackageXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 See [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Configuration Manager uses a driver catalog to manage the different computers, devices, and associated Windows device drivers that it supports. For more information, see [About the Driver Catalog](http://go.microsoft.com/fwlink/?LinkID=110504).  

 You can create an `SMS_Driver` object by using the [CreateFromINF Method in Class SMS_Driver](../../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md) and [CreateFromOEM Method in Class SMS_Driver](../../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md) methods. You use [CreateFromINF Method in Class SMS_Driver](../../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md) to create an `SMS_Driver` Object from a Windows driver INF file. For more information see, How to Import a Windows Driver Described by an INF File into Configuration Manager. You use [CreateFromOEM Method in Class SMS_Driver](../../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md) to create an `SMS_Driver` object from a Txtsetup.oem file.  

 Drivers share many of the abstract qualities of configuration items but you cannot use drivers like configuration items. For example, they cannot be assigned to baselines.  

 Drivers can be arranged into categories by adding the relevant category identifier to the `SMS_Driver Server WMI Class``CategoryInstance_UniqueIDs` array property. For more information, see How to Add a Category to a Windows Driver.  

 When you use the Configuration Manager server WMI classes in your application or script, remember that each driver must be added to at least one driver package ([UPDATED: SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)) before it can be installed on a client. For more information, see How to Create a Driver Package for a Windows Driver in Configuration Manager. Mass storage drivers may also be added to a boot image package, represented by [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md). How to add a Windows Driver to a Configuration Manager Boot Image Package.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [UPDATED: SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [SMS_Driver_Details Server WMI Class](../../../develop/reference/osd/sms_driver_details-server-wmi-class.md)   
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)
