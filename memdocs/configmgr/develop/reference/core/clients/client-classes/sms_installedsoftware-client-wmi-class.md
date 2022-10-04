---
title: SMS_InstalledSoftware Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_InstalledSoftware class is a client WMI class that merges installed software information from multiple sources to provide categorization and Microsoft Licensing information.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f9dd9d35-1162-46c2-b198-5278e706012f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_InstalledSoftware Client WMI Class
The `SMS_InstalledSoftware` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that merges installed software information from multiple sources to provide categorization and Microsoft Licensing information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InstalledSoftware     
{    
      String ARPDisplayName;    
      String ChannelCode;    
      String CM_DSLID;    
      String EvidenceSource;   
      DateTime InstallDate;    
      UInt32 InstallDirectoryValidation;    
      String InstalledLocation;    
      String InstallSource;    
      UInt32 InstallType;   
      UInt32 Language;    
      String LocalPackage;    
      String ProductCode;    
      String ProductID;    
      String ProductName;    
      String ProductVersion;    
      String Publisher;    
      String RegisteredUser;    
      String ServicePack;    
      String SoftwareCode;    
      String SoftwarePropertiesHash;    
      String SoftwarePropertiesHashEx;    
      String UninstallString;    
      String UpgradeCode;    
      UInt32 VersionMajor;    
      UInt32 VersionMinor;    
};  
```  

## Methods  
 The `SMS_InstalledSoftware` class does not define any methods.  

## Properties  
 `ARPDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The product display name as found in **Add or Remove Programs**. An example name is "Microsoft SQL Server 2005 Tools".  

 `ChannelCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Numeric code that represents the channel through which the software product was acquired. Possible values are:  

| Value | Description |
| ----- | ----------- |
|0|Full Packaged Product (Retail)|  
|1|Compliance Checked Product|  
|2|OEM|  
|3|Volume|  

> [!NOTE]
>  Other values are undefined.  

 `CM_DSLID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Reserved. For future use.  

 `EvidenceSource`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SMS_Report (TRUE)]  

 Describes how this software was discovered.  

|Value|Description|  
|-----------|-----------------|  
|A|Windows Installer|  
|B|The software's install registry key|  
|C|The software's uninstall registry key|  
|D|Operating System's Windows Installer|  
|E|Operating System's Windows NT registry setting|  
|M|Internally computed property|  
|X|Unknown|  

 `InstallDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Date and time of when the software product was installed.  

 `InstallDirectoryValidation`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Numeric code that provides additional information about the inventoried software. Possible values are:  

| Value | Description |
| ----- | ----------- |
|1|Because the `InstalledLocation` property was not available in any of the data sources, a check was not possible.|  
|2|An executable file was found in the directory specified by the `InstalledLocation` property or in one of its subdirectories.|  
|3|A file was found in the directory specified by the `InstalledLocation` property or in one of its subdirectories, but no executable file was found.|  
|4|The directory specified by the `InstalledLocation` property was located, but it did not contain any executable files or other files.|  
|5|The directory specified by the `InstalledLocation` property does not exist.|  

 `InstalledLocation`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The full path to the primary directory that is associated with the software.  

 `InstallSource`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The full path of the directory from which the software was installed, for example, \\\Software\Microsoft\SMS\Setup.exe.  

 `InstallType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [SMS_Report (TRUE)]  

 Describes the type of software that has been installed.  

|Value|Description|  
|-----------|-----------------|  
|0|Physically installed|  
|1|Virtually installed|  

 `Language`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The language associated with the software product.  

 `LocalPackage`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The local cached package, for example, C:\Windows\Installer\9c1c748.msi.  

 `ProductCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique identifier for the particular product release. The identifier is represented as a GUID for Windows Installer-based applications or as the string used by the product to register with **Add or Remove Programs**.  

 `ProductID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Vendor-generated ID that uniquely identifies the product.  

 `ProductName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the installed product that is displayed to the user, for example, "Microsoft Office 2003".  

 `ProductVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The version of the product, for example, "5.1.1969".  

 `Publisher`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The company that publishes the software.  

 `RegisteredUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The registered user for the product.  

 `ServicePack`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The major version number of the service pack that is installed on the computer. If no service pack has been installed, the value is 0 (zero). Applicable only to operating systems.  

 `SoftwareCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 A normalized version of the `ProductCode` property. All characters in the string are lowercase.  

 `SoftwarePropertiesHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature derived from a combination of the `ProductName`, `Publisher`, and `ProductVersion` properties of the software product.  

 `SoftwarePropertiesHashEx`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature derived from a combination of the `ProductName`, `Publisher`, `ProductVersion`, and `Language` properties of the software product.  

 `UninstallString`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The uninstall string as registered by the product with **Add or Remove Programs**, for example, "MsiExec.exe /X{210C4411-95A8-4CAF-8B23-F964CF8A78F3}".  

 `UpgradeCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A GUID that represents a related set of products. Applicable only to Windows Installer-based products.  

 `VersionMajor`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The major product version that is derived from the `ProductVersion` property.  

 `VersionMinor`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The minor product version that is derived from the `ProductVersion` property.  

## Remarks  
 This class merges information from as many as five sources. The first source is the Windows `MsiEnumProducts` function. This function enumerates through all the products that are currently advertised or installed. Other sources of information for all installed software are the following registry keys:  

- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\UserData\\[User SID]\Products  

- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall  

  The class also gathers information for operating system software from the following sources:  

- WMI class root\CIMV2:Win32_OperatingSystem  

- Registry key HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_BrowserHelperObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledExecutable Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
