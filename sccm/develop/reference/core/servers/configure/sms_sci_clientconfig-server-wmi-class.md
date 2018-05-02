---
title: "SMS_SCI_ClientConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cad6e82b-ba60-4252-8336-f83d595b69bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SCI_ClientConfig Server WMI Class
The `SMS_SCI_ClientConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents general configuration information that can be used by more than one client component.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_ClientConfig : SMS_SiteControlItem   
{  
     String ClientConfigName;  
     UInt32 FileType;  
     UInt32 Flags;  
     String ItemName;  
     String ItemType;  
     String Platforms[];  
     SMS_EmbeddedPropertyList PropLists[];  
     SMS_EmbeddedProperty Props[];  
     SMS_Client_Reg_MultiString_List RegMultiStringLists[];  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SCI_ClientConfig` class does not define any methods.  

## Properties  
 `ClientConfigName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [StringEnumeration]  

 Name of the client configuration block. Currently the only defined value is COMP_STATUS_MESSAGE_FILTER (Component Status Message Filter).  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags identifying the configuration block. Possible values are listed below. The default value is 0.  

 1  
 ACTIVE  

 2  
 BASE_INSTALL  

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

 `Platforms`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: [StringEnumeration]  

 This property is obsolete.  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the configuration.  

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the configuration.  

 `RegMultiStringLists`  
 Data type: `SMS_Client_Reg_MultiString_List` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md) objects for the configuration.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Run the following query for a complete list of client configuration components defined for your site server.  

```  
SELECT * FROM SMS_SCI_ClientConfig  
WHERE SiteCode = "<sitecode>"  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md)   
 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
