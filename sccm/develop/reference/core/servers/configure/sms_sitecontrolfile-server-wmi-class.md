---
title: "SMS_SiteControlFile Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 06c30f1a-fb2a-49c0-863c-6cf8adf3d162
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SiteControlFile Server WMI Class
The `SMS_SiteControlFile` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the site control file and contains methods to maintain version control of the site control file.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteControlFile : SMS_BaseClass   
{  
     String BuildNumber;  
     UInt32 FileType;  
     String FormatVersion;  
     String SCFData;  
     UInt32 SerialNumber;  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SiteControlFile` class does not define any methods.  

## Properties  
 `BuildNumber`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Build number of the Configuration Manager installation that create the site control file. The default value is "".  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 This property is deprecated.  

 `FormatVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Version of the site control file format. The default value is "".  

 `SCFData`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy, large]  

 Current site control file data in text format (accumulated deltas).  

 `SerialNumber`  
 Data type: `UInt32`  

 Access type: ReadWrite  

 Qualifiers: [key]  

 Unique ID of the file itself. The number is incremented every time the file changes. The default value is 0.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read, SizeLimit("3")]  

 Site code of the site associated with the site control file. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application uses the methods of this class to perform version control of the site control file. To update the contents of the site control file, the application should use classes derived from [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
