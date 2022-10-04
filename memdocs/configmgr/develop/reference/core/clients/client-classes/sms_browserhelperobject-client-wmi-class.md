---
title: SMS_BrowserHelperObject Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_BrowserHelperObject class is a client Windows Management Instrumentation class  that enumerates all browser helper objects on a computer.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9a0597a0-4bb2-47a7-b77e-8b57ca4afb4e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_BrowserHelperObject Client WMI Class
The `SMS_BrowserHelperObject` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that enumerates all browser helper objects on a computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BrowserHelperObject   
{  
      String BinFileVersion;  
      String BinProductVersion;  
      String CLSID;  
      String Description;  
      String FileName;  
      String FilePropertiesHash;  
      String FilePropertiesHashEx;  
      String FileVersion;  
      String Product;  
      String ProductVersion;  
      String Publisher;  
      String Version;  
};  
```  

## Methods  
 The `SMS_BrowserHelperObject` class does not define any methods.  

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

 `CLSID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The COM class ID that is associated with the browser helper object.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 File description that can be presented to users, for example, "Groove Shell Extensions Module".  

 `FileName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the file, including the extension but excluding the path, for example, "GrooveShellExtensions.dll".  

 `FilePropertiesHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 A unique 128-bit signature that is derived from a combination of the `Product`, `Description`, `ProductVersion`, `Publisher`, and `FileName` properties of the file.  

 `FilePropertiesHashEx`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature that is derived from a combination of the `Product`, `Description`, `ProductVersion`, `Publisher`, `FileName`, `FileVersion`, `BinProductVersion`, and `BinFileVersion` properties of the file.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The version of the file, for example, "12.0.4518.1014".  

 `Product`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the product with which the file is distributed, for example, "Microsoft Windows".  

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

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Reserved. For internal use.  

## Remarks  
 Many users install applications from the Web unintentionally or through various deceptive practices. Browser helper objects allow extensions to the Internet Explorer browser. These extensions typically appear as toolbars in the user interface. Most software that is considered malware is in this form.  

 This class enumerates all the subkeys of HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects, gathering a set of class identifiers that are used to retrieve useful information from a second lookup in the HKEY_CLASSES_ROOT\CLSID\\[retrieved bho id]\InprocServer32 hive. Enumeration of the subkeys provides a list of the binaries from which the header information can be retrieved.  

> [!NOTE]
>  When constructing the `FilePropertiesHash` property, if the header data for the executable file is `null` for the company, product, or version field, the file name in uppercase is substituted for the field.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_InstalledExecutable Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
