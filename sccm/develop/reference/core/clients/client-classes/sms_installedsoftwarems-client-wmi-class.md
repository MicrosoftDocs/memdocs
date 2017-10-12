---
title: "SMS_InstalledSoftwareMS Class"
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
ms.assetid: 3d13ea8d-dd55-4b85-bb54-596b677366c5searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_InstalledSoftwareMS Client WMI Class
> [!IMPORTANT]
>  This class is no longer used in System Center Configuration Manager.  

 The `SMS_InstalledSoftwareMS` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that merges Microsoft-specific installed software information from multiple sources to provide categorization and Microsoft Licensing information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InstalledSoftwareMS   
{  
      String ChannelCode;  
      String ChannelID;  
      String MPC;  
      String ProductCode;  
      String SoftwareCode;  
};  
```  

## Methods  
 The `SMS_InstalledSoftwareMS` class does not define any methods.  

## Properties  
 `ChannelCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The procurement channel for the product. Possible values are:  

|||  
|-|-|  
|0|Full Packaged Product|  
|1|Compliance Checked Product|  
|2|OEM|  
|3|Volume|  

 `ChannelID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Three-digit ID that is also used to indicate the channel as obtained from the `ProductID` property for Microsoft products. The specific values vary by product.  

 `MPC`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Unique five-digit Microsoft Product Code that identifies a specific product family, version, language, and target operating system.  

 `ProductCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique code for the particular product release. This code is represented as a GUID for Microsoft Windows Installer based applications or as the string used by the product to register with **Add or Remove Programs**.  

 `SoftwareCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 A standardized version of the `ProductCode` property. All characters in the string are lowercase.  

## Remarks  
 This class merges information from as many as five sources. The first source is the Microsoft Windows `MsiEnumProducts` function. This function enumerates through all the products that are currently advertised or installed. Other sources of information for all installed software are the following registry keys:  

-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\UserData\\[User SID]\Products  

-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall  

 The class also gathers information for operating system software from the following sources:  

-   WMI class root\CIMV2:Win32_OperatingSystem  

-   Registry key HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion  

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
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SoftwareShortcut Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
