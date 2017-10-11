---
title: "SMS_AutoStartSoftware Class"
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
ms.assetid: 0de5b1e8-b3e0-4c00-80d3-f9e35ffcb40fsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AutoStartSoftware Client WMI Class
The `SMS_AutoStartSoftware` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that enumerates software that starts automatically with, or immediately after, the operating system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AutoStartSoftware   
{  
      String BinFileVersion;  
      String BinProductVersion;  
      String Description;  
      String FileName;  
      String FilePropertiesHash;  
      String FilePropertiesHashEx;  
      String FileVersion;  
      String Location;  
      String Product;  
      String ProductVersion;  
      String Publisher;  
      String StartupType;  
      String StartupValue;  
};  
```  

## Methods  
 The `SMS_AutoStartSoftware` class does not define any methods.  

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

 File description to be presented to users, for example, "Keyboard driver for AT-style keyboards" or "Microsoft Word for Windows".  

 `FileName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the file, including the extension but excluding the path, for example, "Notepad.exe".  

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

 The version of the file, for example, "3.00A" or "5.00.RC2".  

 `Location`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The path where the autostart file was discovered. This path is relative to the value of the `StartupType` property. For example, it can be "Software\Microsoft\Windows\CurrentVersion\Run" when the `StartupType` property is set to "HKEY_LOCAL_MACHINE".  

 `Product`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The name of the product with which the file is distributed, for example, "Microsoft Windows".  

 `ProductVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The version of the product with which the file is distributed, for example, "3.00A" or "5.00.RC2".  

 `Publisher`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The company that produced the file, for example, "Microsoft Corporation" or "Standard Microsystems Corporation, Inc.".  

 `StartupType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The point from which the software is automatically launched. Possible values are:  

-   Registry:Current User  

-   Registry:Local Machine  

-   Win.ini  

-   All Users Startup Folder  

-   User Profile Startup Folder  

 `StartupValue`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The application command string that is associated with the shortcut.  

## Remarks  
 Much system-dependent software is loaded separately from the system due to the nature of the application. Most software requires the operating system to be running before being loaded. Along with many applications intended for useful purposes, such as sound driver, mouse driver, and other interfaces, items such as malware and viruses tend to place themselves within the same load areas. You can enumerate these applications to monitor the health of some of their security policies and procedures.  

 There are eight areas in the registry where applications can be run at the startup of the operating system. Enumeration of the following keys provides a list of applications and their associated paths from which header information can be retrieved:  

-   HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run  

-   HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce  

-   HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnceEx  

-   HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\run  

-   HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\load  

-   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run  

-   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce  

-   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnceEx  

 The `SMS_AutoStartSoftware` class enumerates all items in the %*systemdir*%\Win.ini file, to identify older applications in addition to malicious software that might use this nontraditional method of activation. This class enumerates applications in the following file entries:  

-   win.ini [windows] run=  

-   win.ini [windows] load=  

 The `SMS_AutoStartSoftware` class enumerates the contents of the **Startup** folder in the **Start** menu to provide the path to the binaries from which header information can be retrieved. If the binary is Rundll32.exe or Rundll64.exe, then the class retrieves the header information from the DLL file that is the first command line parameter for execution of Rundll32.exe.  

 For example:  

```  
RUNDLL32.EXE C:\WINDOWS\System32\NvCpl.dll,NvStartup  
```  

 In this case, the class gathers the header information from NVCpl.dll, instead of Rundll32.exe.  

> [!NOTE]
>  If the header data for the executable file is `null` for the company, product, or version field, then the file name in uppercase is substituted for the field.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_BrowserHelperObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledExecutable Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
