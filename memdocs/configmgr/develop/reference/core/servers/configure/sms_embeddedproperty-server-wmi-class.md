---
title: SMS_EmbeddedProperty Class
titleSuffix: Configuration Manager
description:  An SMS Provider that represents a general-purpose embedded property. The property is used by the site control file to define the properties of a site control item.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3086e816-3a2a-437b-a61f-1b0a2f04082d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_EmbeddedProperty Server WMI Class
The `SMS_EmbeddedProperty` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a general-purpose embedded property used by the site control file to define the properties of a site control item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_EmbeddedProperty  
{  
     String ItemType;  
     String PropertyName;  
     UInt32 Value;  
     String Value1;  
     String Value2;  
};  
```  

## Methods  
 The `SMS_EmbeddedProperty` class does not define any methods.  

## Properties  
 `ItemType`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Property token item, site control file.  

 `PropertyName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the property. The name is case sensitive and might contain several words, such as "Startup Schedule". The default value is "".  

 `Value`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 A numeric value if the property is numeric. The default value is 0.  

 `Value1`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 A string value if the property is a string. The value is a registry data type if the property comes from the system registry. Otherwise, the value is the actual string for the property. The default value is "".  

 `Value2`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 A value to indicate the string value of the property if `Value1` indicates a `REG_SZ` registry data type. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Some properties contain multiple property values and store values in both `Value1` and `Value2`. Properties that contain multi-string registry data types use the [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md).  

  There is no list that defines the properties for each site control item. Property names that contain the word "Reserved" cannot be modified.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
