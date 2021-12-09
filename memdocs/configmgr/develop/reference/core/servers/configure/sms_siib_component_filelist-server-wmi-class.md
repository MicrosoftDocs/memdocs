---
title: "SMS_SIIB_Component_FileList Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: eccf8bc7-98bf-444d-b66d-6f782dfe355a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SIIB_Component_FileList Server WMI Class
The `SMS_SIIB_Component_FileList` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents file list information for a Configuration Manager component.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_Component_FileList : SMS_SiteInstallItemBase   
{  
     String ComponentName;  
     UInt64 Flags  
     String ItemName;  
     String ItemType;  
     SMS_SII_PropertyList PropLists[];  
     SMS_SII_Property Props[];  
     String SiteCode;  
     String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_Component_FileList` class does not define any methods.  

## Properties  
 `ComponentName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the Configuration Manager component to which the file list corresponds.  

 `Flags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [bits]  

 For internal use only.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: Key  

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

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `Units`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: None  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

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
 [SMS_SII_Property Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_property-server-wmi-class.md)   
 [SMS_SII_PropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_propertylist-server-wmi-class.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
