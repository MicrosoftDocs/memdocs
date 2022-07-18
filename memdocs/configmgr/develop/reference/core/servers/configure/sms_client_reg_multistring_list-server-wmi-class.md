---
title: "SMS_Client_Reg_MultiString_List Class"
titleSuffix: "Configuration Manager"
description: "An SMS Provider server class that represents a list of client registry multi-string items from the site control file."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ff5fa70d-5bea-469d-bc84-a940d6558733
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Client_Reg_MultiString_List Server WMI Class
The `SMS_Client_Reg_MultiString_List` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a list of client registry multi-string items from the site control file.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Client_Reg_MultiString_List  
{  
     String ItemType;  
     String ValueName;  
     String KeyPath;  
     String ValueStrings[];  
};  
```  

## Methods  
 The `SMS_Client_Reg_MultiString_List` class does not define any methods.  

## Properties  
 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Client registry multstring item type.  

 `ValueName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Property name reflected in the system registry key where the multi-string items are stored. The default value is "".  

 `KeyPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Path to the multi-string item. The default value is "".  

> [!NOTE]
>  Do not set this property when updating the `ValueName` property.  

 `ValueStrings`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 List of strings that serve as registry data values. The meaning of the strings is determined by the `ValueName` property.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class behaves the same as [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md). It is used to represent data that is stored in the system registry with the `REG_MULTI_SZ` data type.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)
