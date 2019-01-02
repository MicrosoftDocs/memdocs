---
title: "SMS_SiteInstallItemBase Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8f9b69f0-2642-456f-8bbd-f945cd1be6f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SiteInstallItemBase Server WMI Class
The `SMS_SiteInstallItemBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the abstract base class from which all specific site install item configuration classes are derived.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteInstallItemBase : SMS_SiteInstallItem   
{  
     String ItemName;  
     String ItemType;  
     String Units[];  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SiteInstallItemBase` class does not define any methods.  

## Properties  
 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md).  

 `Units`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Units to install. Possible values are:  

- SMS  

- ADMIN_UI  

- Remote control  

  `SiteCode`  
  Data type: `String`  

  Access type: Read-only  

  Qualifiers: [read]  

  For internal use only.  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Use classes derived from [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md) to view the install map represented by [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md)
