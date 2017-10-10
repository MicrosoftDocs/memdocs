---
title: "SMS_SIIB_Generic_Configuration Class"
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
ms.assetid: 778a6935-63c4-4101-983a-28222492373csearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SIIB_Generic_Configuration Server WMI Class
The `SMS_SIIB_Generic_Configuration` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents generic configuration for Configuration Manager components.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_Generic_Configuration : SMS_SiteInstallItemBase   
{  
   String ConfigurationName;  
   String ItemName;  
   String ItemType;  
   SMS_SII_PropertyList PropLists[];  
   SMS_SII_Property Props[];  
   String Units[];  
   String SiteCode;  
};  
```  

## Methods  
 The `SMS_SIIB_Generic_Configuration` class does not define any methods.  

## Properties  
 `ConfigurationName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the configuration.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `PropLists`  
 Data type: `SMS_SII_PropertyList` Array  

 Access type: Read-only  

 Qualifiers: None  

 [SMS_SII_PropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_propertylist-server-wmi-class.md) objects for the component.  

 `Props`  
 Data type: `SMS_SII_Property` Array  

 Access type: Read-only  

 Qualifiers: None  

 [SMS_SII_Property Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_property-server-wmi-class.md) objects for the component.  

 `Units`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SII_Property Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_property-server-wmi-class.md)   
 [SMS_SII_PropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_propertylist-server-wmi-class.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
