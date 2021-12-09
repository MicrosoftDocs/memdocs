---
title: "SMS_SCFToSCI_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 42f6b479-5515-4f4f-a6c2-9bcc8d33452b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SCFToSCI_a Server WMI Class
The `SMS_SCFToSCI_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates an [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md) object with [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md) objects that make up the current site control file.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCFToSCI_a : SMS_BaseAssociation  
{  
      ref:SMS_SiteControlFile SiteControlFile;  
      ref:SMS_SiteControlItem SiteControlItem;  
};  
```  

## Properties  
 `SiteControlFile`  
 Data type: `ref:SMS_SiteControlFile`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md) object path.  

 `SiteControlItem`  
 Data type: `ref:SMS_SiteControlItem`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md) object path.  

## Remarks  
 Class qualifiers for this class include:  

- Association: ToInstance  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
