---
title: "SMS_SII_Property Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_SII_Property WMI class is an SMS Provider server class that represents a general-purpose storage object for property data that can be represented as a single integer or two strings. 
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 49a8e7c3-78b2-4b20-b5e0-4d93fafcc401
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SII_Property Server WMI Class
The `SMS_SII_Property` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a general-purpose storage object for property data that can be represented as a single integer or two strings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SII_Property : SMS_SiteInstallItem   
{  
     String ItemName;  
     String ItemType;  
     String PropertyName;  
     UInt32 Value;  
     String Value1;  
     String Value2;  
};  
```  

## Methods  
 The `SMS_SII_Property` class does not define any methods.  

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

 `PropertyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the property. The name is case sensitive and might contain several words, for example, "Connection Point".  

 `Value`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 A numeric value if the property is numeric.  

 `Value1`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A string value if the property is a string. The value is a registry data type if the property comes from the system registry. Otherwise, the value is the actual string for the property.  

 `Value2`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A value to indicate the string value of the property if `Value1` indicates a `REG_SZ` registry data type.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md)
