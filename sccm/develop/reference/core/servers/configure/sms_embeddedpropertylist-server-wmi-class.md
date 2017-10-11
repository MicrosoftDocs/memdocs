---
title: "SMS_EmbeddedPropertyList Class"
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
ms.assetid: 5ef2a217-7dd3-41ed-9c27-ad824660a948searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_EmbeddedPropertyList Server WMI Class
The `SMS_EmbeddedPropertyList` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a general-purpose embedded object that defines property lists. The property lists are used by the site control file to define the string array properties of a site control item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_EmbeddedPropertyList   
{  
     String ItemType;  
     String PropertyListName;  
     String Values[];  
}  
```  

## Methods  
 The `SMS_EmbeddedPropertyList` class does not define any methods.  

## Properties  
 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Property list token item, site control file.  

 `PropertyListName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the property list. The name is case sensitive and might contain several words, for example, "Network Connection Accounts". The default value is "".  

 `Values`  
 Data type: `String` Array  

 Access type: Read/Write  

 String values for the property list. For example, "SITE_DEFN_NETWK_CONN_ACCNTS" is the value corresponding to the property list name "Network Connection Accounts". The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 There is no list that defines the properties for each site control item. The best way to determine the properties for each site control item is to follow the steps defined in `Determining Which Site Control Item to Use`. Property names that contain the word Reserved cannot be modified.  

 Arrays of strings that come from the system registry use the [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md) class.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)   
 [Configuration Manager Site Control File](../../../../../develop/core/understand/site-control-file.md)
