---
title: "SMS_BootImagePackage Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c0b861c2-5856-4a5f-bdd4-b8252f8bbd1e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_BootImagePackage Server WMI Class
The `SMS_BootImagePackage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as the unit of distribution for boot image source files that are used to start a computer with Windows Pre-Installation Environment (PE) 2.0 and allow operating system deployment task sequence actions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BootImagePackage : SMS_PackageBaseclass  
{  
      UInt32 ActionInProgress;  
      String AlternateContentProviders;  
      String Architecture;  
      String BackgroundBitmapPath;  
      String ContextID;  
      Boolean DefaultImage;  
      String Description;  
      Boolean EnableLabShell;  
      UInt8 ExtendedData[];  
      UInt32 ExtendedDataSize;  
      UInt32 ForcedDisconnectDelay;  
      Boolean ForcedDisconnectEnabled;  
      UInt32 ForcedDisconnectNumRetries;  
      UInt8 Icon[];  
      UInt32 IconSize;  
      Boolean IgnoreAddressSchedule;  
      String ImageDiskLayout;  
      UInt32 ImageIndex;  
      String ImageOSVersion;  
      String ImagePath;  
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
      UInt32 OptionalComponents[];  
      String PackageID;  
      UInt32 PackageSize;  
      UInt32 PackageType;  
      UInt32 PkgFlags;  
      UInt32 PkgSourceFlag;  
      String PkgSourcePath;  
      String PreExecCommandLine;  
      String PreExecSourceDirectory;  
      String PreferredAddressType;  
      UInt32 Priority;  
      SMS_Driver_Details ReferencedDrivers[];  
      Boolean RefreshPkgSourceFlag;  
      SMS_ScheduleToken RefreshSchedule[];  
      UInt32 ScratchSpace;  
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
 The following table shows the methods in `SMS_BootImagePackage`.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_BootImagePackage](../../../develop/reference/osd/addchangenotification-method-in-class-sms_bootimagepackage.md)|Adds a boot image package change notification.|  
|[AddDistributionPoints Method in Class SMS_BootImagePackage](../../../develop/reference/osd/adddistributionpoints-method-in-class-sms_bootimagepackage.md)|Adds the distribution points for the package.|  
|[DeleteContextID Method in Class SMS_BootImagePackage](../../../develop/reference/osd/deletecontextid-method-in-class-sms_bootimagepackage.md)|Deletes the status queue that is associated with the specified context ID for the boot image package.|  
|[ExportDefaultBootImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/exportdefaultbootimage-method-in-class-sms_bootimagepackage.md)|Finalizes and exports a boot image from a Windows Assessment and Deployment Kit installation source to a specified location.|  
|[GetImageProperties Method in Class SMS_BootImagePackage](../../../develop/reference/osd/getimageproperties-method-in-class-sms_bootimagepackage.md)|Reads all image properties from the specified source .wim file to an XML string.|  
|[QueryOSDBinaryInjectionStatus Method in Class SMS_BootImagePackage](../../../develop/reference/osd/queryosdbinaryinjectionstatus-method-in-class-sms_bootimagepackage.md)|Queries the current status of the injection of operating system deployment binaries.|  
|[RefreshPkgSource Method in Class SMS_BootImagePackage](../../../develop/reference/osd/refreshpkgsource-method-in-class-sms_bootimagepackage.md)|Refreshes the package source at all distribution points, when the package properties have not changed.|  
|[ReloadImageProperties Method in Class SMS_BootImagePackage](../../../develop/reference/osd/reloadimageproperties-method-in-class-sms_bootimagepackage.md)|Reloads image properties from the source .wim file and updates the database.|  
|[SetSourceSite Method in Class SMS_BootImagePackage](../../../develop/reference/osd/setsourcesite-method-in-class-sms_bootimagepackage.md)|Sets the code of the source site for the boot image package.|  
|[Unlock Method in Class SMS_BootImagePackage](../../../develop/reference/osd/unlock-method-in-class-sms_bootimagepackage.md)|Sets the source site to the current site, unlocking the boot image package.|  
|[UpdateDefaultImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/updatedefaultimage-method-in-class-sms_bootimagepackage.md)|Creates a copy of the WIM image pointed to by the ImagePath property and injects it with OSD files for boot image deployment.|  
|[UpdateImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/updateimage-method-in-class-sms_bootimagepackage.md)|Creates a copy of the image for the boot image package and updates the image with files for boot image deployment.|  
|[UpdateOptionalComponents Method in Class SMS_BootImagePackage](../../../develop/reference/osd/updateoptionalcomponents-method-in-class-sms_bootimagepackage.md)|Updates all specified optional components to the boot image.|  

## Properties  
 `Architecture`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Architecture of the boot image. The following values are the possible values. The default value is "".  

|||  
|-|-|  
|x86|I386 32-bit microprocessor|  
|ia64|Itanium 64-bit microprocessor|  
|x64|X86-64 64-bit microprocessor|  

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

 `BackgroundBitmapPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Universal Naming Convention (UNC) path of the WinPE background bitmap. Your application can set this property to use a custom bitmap by supplying the path to the custom bitmap files.  

 `ContextID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A context ID that can be queried for the status of injecting operating system deployment binaries. The injection operation takes quite a while, and your application can use this property for periodic status. The default value is "".  

 `DefaultImage`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if this is a default boot image. The default value is `false`.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `EnableLabShell`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if command line support is enabled. The default value is `false`.  

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

 An XML string of disk layout information for the source image, represented by a .wim file (WIM format). The default value is "".  

 `ImageIndex`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Not used for a boot image.  

 `ImageOSVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Operating system version for the default image in the boot WIM file.  

 `ImagePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Original image source path. Configuration Manager uses this path internally when the administrator imports an image. When the image is imported, Configuration Manager injects it with operating system deployment binaries.  

 `ImageProperty`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 An XML string holding metadata of the source .wim file, for example, the version. The default value is "".  

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

 `OptionalComponents`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A list of identifiers of optional components that will be enabled in WinPE. Possible values are:  

|Identifier|Component|  
|----------------|---------------|  
|1|WinPE-DismCmdlets|  
|2|WinPE-Dot3Svc|  
|3|WinPE-EnhancedStorage|  
|4|WinPE-FMAPI|  
|5|WinPE-FontSupport-JA-JP|  
|6|WinPE-FontSupport-KO-KR|  
|7|WinPE-FontSupport-ZH-CN|  
|8|WinPE-FontSupport-ZH-HK|  
|9|WinPE-FontSupport-ZH-TW|  
|10|WinPE-HTA|  
|11|WinPE-StorageWMI|  
|12|WinPE-LegacySetup|  
|13|WinPE-MDAC|  
|14|WinPE-NetFx4|  
|15|WinPE-PowerShell3|  
|16|WinPE-PPPoE|  
|17|WinPE-RNDIS|  
|18|WinPE-Scripting|  
|19|WinPE-SecureStartup|  
|20|WinPE-Setup|  
|21|WinPE-Setup-Client|  
|22|WinPE-Setup-Server|  
|23|Not applicable|  
|24|WinPE-WDS-Tools|  
|25|WinPE-WinReCfg|  
|26|WinPE-WMI|  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

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

 For this class, the package type is PKG_TYPE_BOOTIMAGE (258).  

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

 `PreExecCommandLine`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Command-line for the pre-execution hook injected into WinPE.  

 `PreExecSourceDirectory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 UNC path of pre-execution hook the source directory injected into WinPE.  

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

 `ReferencedDrivers`  
 Data type: `SMS_Driver_Details` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Array of details about Configuration Manager drivers included in the boot image for import.  

 `RefreshPkgSourceFlag`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: [max(15), lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ScratchSpace`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Specifies the amount of available scratch space in WinPE. Possible values are:  

|Megabytes|  
|---------------|  
|32|  
|64|  
|128|  
|256|  
|512|  

 For additional information see [Windows PE Servicing Command-Line Options](http://go.microsoft.com/fwlink/?LinkId=272891).  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

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

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
