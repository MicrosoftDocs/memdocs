---
title: SMS_InstalledExecutable Class
titleSuffix: Configuration Manager
description: The SMS_InstalledExecutable class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that identifies executable files associated with a software installation.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 31fa9595-6ece-4fc0-a6b2-d8eb280f0cc1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_InstalledExecutable Client WMI Class
The `SMS_InstalledExecutable` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that identifies executable files associated with a software installation.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InstalledExecutable  
{  
      String BinFileVersion;  
      String BinProductVersion;  
      String Description;  
      String ExecutableName;  
      String FilePropertiesHash;  
      String FilePropertiesHashEx;  
      UInt32 FileSize;  
      String FileVersion;  
      Boolean HasPatchAdded;  
      String InstalledFilePath;  
      Boolean IsSystemFile;  
      Boolean IsVitalFile;  
      UInt32 Language;  
      String Product;  
      String ProductCode;  
      String ProductVersion;  
      String Publisher;  
};  
```  

## Methods  
 The `SMS_InstalledExecutable` class does not define any methods.  

## Properties  
 `BinFileVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Reserved. For internal use.  

 `BinProductVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Reserved. For internal use.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 File description that can be presented to users, for example, "Keyboard driver for AT-style keyboards" or "Microsoft Word for Windows".  

 `ExecutableName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Name of the file, including the extension but excluding the path, for example, "Notepad.exe".  

 `FilePropertiesHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature that is derived from a combination of the `Product`, `Description`, `ProductVersion`, `Publisher`, and `FileName` properties of the file.  

 `FilePropertiesHashEx`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature that is derived from a combination of the `Product`, `Description`, `ProductVersion`, `Publisher`, `FileName`, `FileVersion`, `BinProductVersion`, and `BinFileVersion` properties of the file.  

 `FileSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Size of the file, in bytes.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The version of the file, for example, "12.0.4518.1014".  

 `HasPatchAdded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the file was added as part of an update to the product to which it belongs.  

 `InstalledFilePath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The path where the file is located, for example, "C:\Program Files\Microsoft Office".  

 `IsSystemFile`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the file is a system file.  

 `IsVitalFile`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the file is vital for the accurate operation of the product to which it belongs.  

 `Language`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 ID of the language for which the file is intended, for example, "1033".  

 `Product`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the product with which the file is distributed, for example, "Microsoft Windows".  

 `ProductCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 GUID that is the principal identifier for an application or product. For more information, see the Microsoft Windows Installer documentation.  

 `ProductVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The version of the product with which the file is distributed, for example, "4.2.0.2623".  

 `Publisher`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The company that produced the file, for example, "Microsoft Corporation" or "Standard Microsystems Corporation, Inc.".  

## Remarks  

> [!NOTE]
>  This class is not currently used to support existing Asset Intelligence reports. However, it can be enabled to support custom reports.  

 This class identifies executable files associated with a software installation to:  

- Confirm that the application is installed by looking at Configuration Manager file inventory.  

- Indicate what metering rules, based on the executable files, have to be set to meter the application.  

- Perform an application impact analysis.  

  Because the Windows Installer (.msi) file contains a record of the installed executable files, it can be used as the source for the mapping between installed applications and executable files.  

  This class retrieves data from two sources. For each [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md) object, the class identifies the .msi package by looking in the `LocalPackage` property, and queries the .msi database for all .exe and .com files.  

  For any [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md) object that has the `LocalPackage` property set to `null`, the `SMS_InstalledExecutable` class inventories all executable files in the directory that are identified by the `InstallLocation` property. Executable files that are installed outside of the main installation directory are not inventoried.  

> [!NOTE]
>  This class does not inventory executable files located in the %*windir*% and %*systemroot*% directories.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_BrowserHelperObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
