---
title: "SMS_SoftwareShortcut Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_SoftwareShortcut class is a client Windows Management Instrumentation class that defines a shortcut to executable files or a shortcut in a common system location."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a65b6385-f80f-4aa2-8e55-b8dc119e9673
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SoftwareShortcut Client WMI Class
The `SMS_SoftwareShortcut` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that defines a shortcut to executable files or a shortcut in a common system location.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareShortcut  
{  
      String BinFileVersion;  
      String BinProductVersion;  
      String Description;  
      String FilePropertiesHash;  
      String FilePropertiesHashEx;  
      UInt32 FileSize;  
      String FileVersion;  
      UInt32 Language;  
      String ParentName;  
      String Product;  
      String ProductCode;  
      String ProductVersion;  
      String Publisher;  
      String ShortcutKey;  
      String ShortcutName;  
      UInt32 ShortcutType;  
      String TargetExecutable;  
};  
```  

## Methods  
 The `SMS_SoftwareShortcut` class does not define any methods.  

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

 File description that can be presented to users, for example, "Microsoft Word for Windows".  

 `FilePropertiesHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature that is derived from a combination of the `Product`, `Description`, `ProductVersion`, `Publisher`, and `FileNam`e properties of the file.  

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

 `Language`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Language associated with the file, for example, "1033".  

 `ParentName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the shortcut container, for example, "Start Menu", "Quick Launch", or "Desktop".  

 `Product`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the product with which the file is distributed, for example, "Microsoft Windows".  

 `ProductCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

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

 `ShortcutKey`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: Key  

 Key for the shortcut, without the full path.  

 `ShortcutName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the shortcut, without the full path.  

 `ShortcutType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The type of shortcut. Possible values are:  

| Value | Shortcut type |
| ----- | ------------- |
|1|Shortcut to Folder|  
|2|Shortcut to File (EXE or DLL)|  
|3|Application Reference (.appref-ms)|  

 `TargetExecutable`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the executable file that is linked to the shortcut.  

## Remarks  

> [!NOTE]
>  This class is not currently used to support existing Asset Intelligence reports. However, it can be enabled to support custom reports.  

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
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
