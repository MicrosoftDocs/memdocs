---
description: Learn how to represent a Configuration Manager server component installed on one or more servers at a site.
title: SMS_SCI_Component Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f73ab9ee-0b2b-4e98-bebb-dbd982ac5424
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SCI_Component Server WMI Class
The `SMS_SCI_Component` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a Configuration Manager server component installed on one or more servers at a site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_Component : SMS_SiteControlItem   
{  
     String ComponentName;  
     UInt32 FileType;  
     UInt32 Flag;  
     String ItemName;  
     String ItemType;  
     String Name;  
     SMS_EmbeddedProperty Props[];  
     SMS_EmbeddedPropertyList PropLists[];  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SCI_Component` class does not define any methods.  

## Properties  
 `ComponentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the Configuration Manager server component. The default value is "".  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Flag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flag identifying the component. Possible values are listed below. The default value is NAMED_SERVER_INSTALLED (6).  

|Value|Description|  
|-----------|-----------------|  
|1|ROLE_NOT_INSTALLED. If the flag is set to this value, the `Name` property specifies the server role. The component is installed on every server having the specified role.|  
|2|NAMED_SERVER_NOT_INSTALLED. If the flag is set to this value, the `Name` property specifies a particular server on which the component is installed. The server name does not include backslashes.|  
|5|ROLE_INSTALLED. If the flag is set to this value, the `Name` property specifies the server role. The component is installed on every server having the specified role.|  
|6|NAMED_SERVER_INSTALLED. If the flag is set to this value, the `Name` property specifies a particular server on which the component is installed. The server name does not include backslashes.|  

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

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Configuration Manager role or server name, depending on the value of `Flag`. The default value is "".  

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the component.  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the component.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Run the following query for a complete list of Configuration Manager server components defined for your site server.  

```  
SELECT * FROM SMS_SCI_Component  
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
