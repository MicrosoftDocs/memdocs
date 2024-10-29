---
title: SMS_SiteControlItem Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_SiteControlItem WMI class is an SMS Provider server class that represents the abstract base class for all site control item classes.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a0d437e7-2534-431c-943c-9cec4e70cf49
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SiteControlItem Server WMI Class
The `SMS_SiteControlItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the abstract base class for all site control item classes.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteControlItem : SMS_BaseClass   
{  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SiteControlItem` class does not define any methods.  

## Properties  
 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 The property is deprecated.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique name identifying the site control item within items of the same type. The default value is "".  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique type of the site control item. The default value is "".  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 Unique three-letter site code identifying the site. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses classes derived from this class to read and update items in the site control file. These classes are named with the prefix "SMS_SCI_". An example of a derived class is [SMS_SCI_Address Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_address-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
