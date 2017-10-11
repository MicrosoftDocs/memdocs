---
title: "SMS_SCI_FileDefinition Class"
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
ms.assetid: d8a6be76-8006-4237-881e-547b757bce7csearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SCI_FileDefinition Server WMI Class
The `SMS_SCI_FileDefinition` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the basic properties of the site control file.  

> [!NOTE]
>  This class is vital to the operation of the site control infrastructure. Changing the values for an existing site might render the site control file unusable for further configuration. Existing objects for functioning sites should not be changed.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_FileDefinition : SMS_SiteControlItem   
{  
     String Comment;  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     String OriginatingSite;  
     UInt32 SerialNumber;  
     String SiteCode;  
     String TargetSite;  
};  
```  

## Methods  
 The `SMS_SCI_FileDefinition` class does not define any methods.  

## Properties  
 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Free-format comment. The default value is "".  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `OriginatingSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Site that originated the creation of the value indicated by `TargetSite`. The default value is "".  

 `SerialNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Serial number of the actual site control file. It is incremented each time the site control file changes.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `TargetSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Site for which you are creating the site control file. The default value is "".  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
