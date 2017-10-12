---
title: "SMS_SiteToSiteID_a Class"
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
ms.assetid: b3b16194-ddd8-4407-8f8b-b6f375f3e89dsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SiteToSiteID_a Server WMI Class
The `SMS_SiteToSiteID_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object with an [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) object representing identifying information for the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteToSiteID_a : SMS_BaseAssociation  
{  
      ref:SMS_Site site;  
      ref:SMS_Identification siteIdentification;  
};  
```  

## Methods  
 The `SMS_SiteToSiteID_a` class does not define any methods.  

## Properties  
 `site`  
 Data type: `ref:SMS_site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object path for the site.  

 `siteIdentification`  
 Data type: `ref:SMS_Identification`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) object path for the site identification.  

## Remarks  
 Class qualifiers for this class include:  

-   Association: ToInstance  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
