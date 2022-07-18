---
title: "SMS_Package Class"
titleSuffix: "Configuration Manager"
description: The SMS_Package Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that contains information about Configuration Manager packages.
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 59e73a1c-ff5a-485c-bff7-41aab12e5623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Package Server WMI Class
The `SMS_Package` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains information about Configuration Manager packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Package : SMS_PackageBaseclass  
{  
      UInt32 ActionInProgress;  
      String AlternateContentProviders;  
      SInt32 DefaultImageFlags;  
      String Description;  
      UInt8 ExtendedData[];  
      UInt32 ExtendedDataSize;  
      UInt32 ForcedDisconnectDelay;  
      Boolean ForcedDisconnectEnabled;  
      UInt32 ForcedDisconnectNumRetries;  
      UInt8 Icon[];  
      UInt32 IconSize;  
      Boolean IgnoreAddressSchedule;  
      Boolean IsPredefinedPackage;  
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
      DateTime TransformAnalysisDate;  
      UInt32 TransformReadiness;  
      String Version;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_Package` class.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/addchangenotification-method-in-class-sms_package.md)|Adds a package change notification.|  
|[AddDistributionPoints Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/adddistributionpoints-method-in-class-sms_package.md)|Adds the distribution points for the package.|  
|[CheckDuplicateShareName Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/checkduplicatesharename-method-in-class-sms_package.md)|Determines if any other package is using the same custom share name.|  
|[CheckDuplicateSourceName Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/checkduplicatesourcename-method-in-class-sms_package.md)|Determines whether the specified source name is used by another package.|  
|[CheckPackageShareForTaskSequenceDeployment Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/checkpackagesharefortasksequencedeployment-method-in-class-sms_package.md)|Checks whether the package share type meets the requirements of a task sequence deployment.|  
|[RefreshPkgSource Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/refreshpkgsource-method-in-class-sms_package.md)|Refreshes the package source at all distribution points, when the package properties have not changed.|  
|[SetSourceSite Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/setsourcesite-method-in-class-sms_package.md)|Sets the code of the source site for the package.|  
|[Unlock Method in Class SMS_Package](../../../../../develop/reference/core/servers/configure/unlock-method-in-class-sms_package.md)|Sets the source site to the current site, unlocking the package.|  

## Properties  
 `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `DefaultImageFlags`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 A flag that indicates the package type. Possible values are:  

|Value|Package type|  
|-|-|  
|2|USMT|  

> [!WARNING]
>  Currently only the USMT package type is defined, all of other package types are 0.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

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

 `IsPredefinedPackage`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 A flag that indicates whether this package is a predefined package.  

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

 `PackageID`  
 Data type: `String`  

 Access type: [key]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageSize`  
 Data type: `UInt32`  

 Access type: Read  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourceFlag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PreferredAddressType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshPkgSourceFlag`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type: Read/Write]  

 Qualifiers: [max(15), lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

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

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

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

 `TransformAnalysisDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date when the package was last analyzed by Package Conversion Manager.  

 `TransformReadiness`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Stores the readiness value as determined by the analyze process in Package Conversion Manager. The default value is 0.  

 Possible values are:  

|Value|Transform readiness|  
|-|-|  
|0|Unknown|  
|1|NotApplicable|  
|2|NotReady|  
|3|Ready|  
|4|Transformed|  
|5|Error|  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Configuration Manager uses packages to distribute software to clients. Every package must contain at least one program ([SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md)), identifying what actions should occur on the client when the package is received. You can also identify whether the program provides an install status Management Information Format (MIF) file to report status or just uses an exit code.  

  When your application deletes an `SMS_Package` object, it is not fully deleted until deletion of its related items, for example, programs, source files, distribution points, and advertisements. Instead, Configuration Manager sets the `ActionInProgress` property to DELETE to mark the package for deletion. In SMS 2.0, to ensure that a query does not retrieve packages that have been marked for deletion, add this case to the WHERE clause. In SMS 2003, the WHERE clause is not required, because packages that are marked for deletion are not retrieved by a query. Use a status MIF file to generate detailed status reporting. To generate a status MIF file, your application must call the InstallStatusMIF function. For more information, see Status MIF Functions.  

  The values that your application provides when creating a package are entirely dependent on the programs that the package contains. For example, if the package contains a simple program that does not use source files and does not generate a status MIF file, the application can create a package that merely contains a value for the `Name` property.  

  Changing the `ShareName` or the `PkgSourcePath` property causes the Distribution Manager to delete and recreate the package on all distribution points of the current site. Because this can be an expensive process, your application should be efficient when updating these fields.  

> [!NOTE]
>  Your application can also use the [GetPDFData Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/getpdfdata-method-in-class-sms_pdf_package.md) to generate an `SMS_Package` object.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)   
 [GetPDFData Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/getpdfdata-method-in-class-sms_pdf_package.md)   
 [How to Create a Package](../../../../../develop/core/servers/configure/how-to-create-a-package.md)   
 [PowerShell Cmdlet: New-CMPackage](/powershell/module/configurationmanager/new-cmpackage)
