---
title: "SMS_PackageBaseclass Class"
titleSuffix: "Configuration Manager"
ms.date: "12/14/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0e172800-3d43-4164-a89f-34489f957c42
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PackageBaseclass Server WMI Class
The `SMS_PackageBaseclass` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as the abstract base class for all packages, for example, [SMS_BootImagePackage Server WMI Class](../../../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md), [SMS_DriverPackage Server WMI Class](../../../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md), and [SMS_SoftwareUpdatesPackage Server WMI Class](../../../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md).  

## Syntax  

```  
Class SMS_PackageBaseclass : SMS_BaseClass  
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
      String ISVString;  
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
 The `SMS_PackageBaseclass` class does not define any methods.  

## Properties  

### ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The current action that is being performed on the package by Configuration Manager. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|NONE|  
|1|UPDATE|  
|2|ADD|  
|3|DELETE|  

### AlternateContentProviders  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 An XML string to set alternate content provider settings. This property does not apply to a software update package or a driver package.  

### Description  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The long description of the package.  

### ExtendedData  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 The XML blob for image deployment.  

### ExtendedDataSize  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size of extended data for the package. The default value is 0.  

### ForcedDisconnectDelay  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The time, in minutes, that Configuration Manager waits before forcibly disconnecting users from the distribution point share. The default value is 5 minutes.  

### ForcedDisconnectEnabled  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if Configuration Manager should forcibly disconnect users from the distribution point share when a share violation occurs while updating, refreshing, or deleting package source files. The default value is `false`.  

> [!NOTE]
>  Enable this property with caution. Forcibly disconnecting users can have adverse effects on the client.  

### ForcedDisconnectNumRetries  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The number of times Configuration Manager attempts to disconnect a user from the distribution point share. The default number of retries is 2.  

### Icon  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large]  

 Optional. Array representing the file that contains the icon to use for the package. If it is used, this icon replaces the default package icon in the Configuration Manager console.  

### IconSize  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size of the icon, in bytes. The default value is 0. Set this property to 0 to clear the icon.  

### IgnoreAddressSchedule  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if Configuration Manager ignores any schedule of the sender specified by `PreferredAddressType`. The default value is `false`.  

### ISVData  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 ISV extensibility data.  

### ISVDataSize  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size, in bytes, of `ISVData`. The default value is 0.  

### ISVString  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 String for partner extensibility.  

### Language  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The language of the package. This property is used with `Manufacturer`, `Name`, and `Version` to identify a package in the console. For example, you might have an English version and a German version of the same package.  

### LastRefreshTime  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last date and time when the package source was refreshed at its distribution points.  

### LocalizedCategoryInstanceNames  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized names of the categories to which the configuration item belongs.  

### Manufacturer  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The manufacturer (publisher) of the package.  

### MIFFilename  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the Management Information Format (MIF) file that contains the package status.  

### MIFName  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the MIF file that contains the program status for the package. The file name extension must be .mif. For more information, see the Remarks section later in this topic.  

### MIFPublisher  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the software publisher of the package.  

### MIFVersion  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The version number of the package.  

### Name  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the package. The default name is "".  

### NumOfPrograms  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The number of programs the package has. The default value is …  

### PackageID  
 Data type: `String`  

 Access type: [key]  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

 ### PackageSize  
 Data type: `UInt32`  

 Access type: Read  

 Size of the package.  

### PackageType  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of the package. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|Regular software distribution package.|  
|3|Driver package.|  
|4|Task sequence package.|  
|5|Software update package.|  
|6|Device setting package.|  
|7|Virtual application package.| 
|8|Application package.| 
|257|Image package.|  
|258|Boot image package.|  
|259|Operating system install package.|
|260|VHD package.|   

### PkgFlags  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags specifying special properties of the package. Possible values are:  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x0100011 (23)|DO_NOT_ENCRYPT_CONTENT_ON_CLOUD. Do not encrypt content on the cloud. <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  
|0x01000000 (24)|DO_NOT_DOWNLOAD. Do not download the package to branch distribution points, as it will be pre-staged.|  
|0x02000000 (25)|PERSIST_IN_CACHE. Persist the package in the cache.|  
|0x04000000 (26)|USE_BINARY_DELTA_REP. Marks the package to be replicated by distribution manager using binary delta replication.|  
|0x10000000 (28)|NO_PACKAGE. The package does not require distribution points.|  
|0x20000000 (29)|USE_SPECIAL_MIF. This value determines if Configuration Manager uses `MIFName`, `MIFPublisher`, and `MIFVersion` for MIF file status matching. Otherwise, Configuration Manager uses `Name`, `Manufacturer`, and `Version` for status matching. For more information, see the Remarks section later in this topic.|  
|0x40000000 (30)|DISTRIBUTE_ON_DEMAND. The package is allowed to be distributed on demand to branch distribution points.|  

### PkgSourceFlag  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flag indicating the method of reading the package source files. Possible values are listed below. The default value is STORAGE_NO_SOURCE (1).  

|Value|Description|  
|-----------|-----------------|  
|0|STORAGE_NEEDS_SPECIFYING. The user specifies the source file storage.|  
|1|STORAGE_NO_SOURCE. The program does not use source files.|  
|2|STORAGE_DIRECT. Take source files directly from the source without compression. Use this flag when the source files are located on the local server or when a Universal Naming Convention (UNC) path has been specified to a persistent storage location.|  
|3|STORAGE_COMPRESS. This flag is obsolete.|  
|4|STORAGE_LOCAL. Take source files from a local source.|  

### PkgSourcePath  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Location of the files of update contents represented by the package. The location can be either a full local path or a UNC path. Make sure that this location contains all the files and subdirectories needed to complete the program, including any scripts.  

### PreferredAddressType  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Preferred sender to use when copying the package source files to distribution points. Possible values are listed below. Configuration Manager determines which sender to use if a value is not specified.  

 - ADDR_NONE()
 - ADR_LAN(MS_LAN)  
 - ADDR_MAPI(MS_MAPI)  
 - ADDR_RAS_ASYNC(MS_ASYNC_RAS)  
 - ADDR_RAS_ISDN(MS_ISDN_RAS)  
 - ADDR_RAS_X25(MS_X25_RAS)  
 - ADDR_RAS_SNA(MS_SNA_RAS)  
 - ADDR_SNA_BATCH(MS_BATCH_SNA)  
 - ADDR_SNA_INTER(MS_INTER_SNA)  
 - ADDR_COURIER(MS_COURIER)  

### Priority  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Sending priority of the package. Possible values are defined for the `Priority` property of [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md).  

### RefreshPkgSourceFlag  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 `true` if Configuration Manager should refresh the package source files. The default value is `false`. This property always contains `false` when read.  

 Setting this property to `true` has the same effect as calling the [RefreshPkgSource Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/refreshpkgsource-method-in-class-sms_package.md).  

 Do not use this property to update the package source files. Instead, use the `RefreshPkgSource` method.  

### RefreshSchedule  
 Data type: `SMS_ScheduleToken` Array  

 Access type: [max(15), lazy]  

 An embedded array of `SMS_ScheduleToken` objects that define when Configuration Manager will update the package source files at the distribution points. You can specify a refresh schedule only when `PkgSourceFlag` is STORAGE_DIRECT.  

### SecuredScopeNames  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 Represents the security scopes that the package belongs to.  

### SedoObjectVersion  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Object version used to compare to the object version in the database when updating the object. If the object version does not match, the update fails.  

### ShareName  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Share to use on the distribution point. The name can include directories. If the directories do not exist, Configuration Manager creates them. You must specify a share name if you set `ShareType` to SHARE_SPECIFIC.  

### ShareType  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of share used by the distribution point when sharing the package. Possible values are listed below, with the default value SHARE_COMMON. If you specify SHARE_SPECIFIC, you must provide a value for `ShareName`.  

|Value|Description|  
|-----------|-----------------|  
|1|SHARE_COMMON|  
|2|SHARE_SPECIFIC|  

### SourceDate  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time the package source files were last updated on the distribution points.  

### SourceSite  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The site code of the site where the package originated.  


### SourceVersion  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The version of the package available at the site. Incremented when the package is updated or the source files are refreshed.  

### StoredPkgPath  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Full path to the location where Configuration Manager stores the compressed version of the source files on the site server. This path is set by Configuration Manager when the value of `PkgSourceFlag` is STORAGE_COMPRESS.  

### StoredPkgVersion  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the compressed source files for the stored package. The default value is 0.  

### Version  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the package.  

## Remarks  
 Class qualifiers for this class include:  

 - Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  If you set the USE_SPECIAL_MIF flag of the `PkgFlags` property, Configuration Manager looks in the %*TEMP*% directory or the %*windir*% directory for the install status MIF file that is specified in the `MIFFileName` property. If Configuration Manager does not find the file, it searches for all MIF files in those directories. A case-insensitive comparison is made of the values for `MIFName`, `MIFPublisher`, and `MIFVersion` to those specified in the MIF file. If a match is found, the status that is specified in the MIF file is used as the install status for the program, which indicates whether the program successfully executed. If Configuration Manager cannot find a match, or if USE_SPECIAL_MIF is not specified, Configuration Manager uses the program exit code to set the install status for the program. An exit code of zero is considered successful. Any other values are considered application-specific error codes.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [How to Create a Package](../../../../../develop/core/servers/configure/how-to-create-a-package.md)   
 [PowerShell Cmdlet: New-CMPackage](http://go.microsoft.com/fwlink/?LinkId=309284)
