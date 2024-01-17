---
title: SMS_SCI_Configuration Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_SCI_Configuration Windows Management Instrumentation class is an SMS Provider server class that represents a configuration item, which is a generic named container of properties and property lists, for a site server component.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 2fae6449-b766-4353-83de-2c1de25e7932
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SCI_Configuration Server WMI Class
The `SMS_SCI_Configuration` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a configuration item, which is a generic named container of properties and property lists, for a site server component.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_Configuration : SMS_SiteControlItem   
{  
     String ConfigurationName;  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     SMS_EmbeddedProperty Props[];  
     SMS_EmbeddedPropertyList PropLists[];  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SCI_Configuration` class does not define any methods.  

## Properties  
 `ConfigurationName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the configuration.  

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

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the configuration.  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the configuration.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Run the following query for a complete list of configuration objects on your site server.  

```  
SELECT * FROM SMS_SCI_Configuration  
WHERE SiteCode = "<sitecode>"  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
