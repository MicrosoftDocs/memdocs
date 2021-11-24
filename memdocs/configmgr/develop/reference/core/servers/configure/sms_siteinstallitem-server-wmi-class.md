---
title: "SMS_SiteInstallItem Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 54aeb316-ce9e-4e81-b06f-fb556d00b7cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SiteInstallItem Server WMI Class
The `SMS_SiteInstallItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the abstract base class of all site install item classes.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteInstallItem : SMS_BaseClass   
{  
     String ItemName;  
     String ItemType;  
};  
```  

## Methods  
 The `SMS_SiteInstallItem` class does not define any methods.  

## Properties  
 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique name identifying a site install item within items of the same type.  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique type identifying a site install item.  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses classes derived from this class to manipulate site install items. These classes are named with the prefix "SMS_SII_". An example of a derived class is [SMS_SII_Property Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_property-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
