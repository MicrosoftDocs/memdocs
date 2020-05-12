---
title: "SMS_SiteToSubSite_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b53378c0-862d-4de3-934e-e6e3033afd59
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# SMS_SiteToSubSite_a Server WMI Class
The `SMS_SiteToSubSite_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines the hierarchy of sites by relating an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object with its subsites.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteToSubSite_a : SMS_BaseAssociation  
{  
      ref:SMS_Site childSite;  
      ref:SMS_Site parentSite;  
};  
```  

## Methods  
 The `SMS_SiteToSubSite_a` class does not define any methods.  

## Properties  
 `childSite`  
 Data type: `ref:SMS_Site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object path for the child site.  

 `parentSite`  
 Data type: `ref:SMS_Site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an `SMS_Site` object path for the parent site.  

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
