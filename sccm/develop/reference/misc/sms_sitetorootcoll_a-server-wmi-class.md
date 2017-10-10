---
title: "SMS_SiteToROOTColl_a Class"
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
ms.assetid: 31aa4a8c-0422-4d65-bd9c-c5006c2bc215searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SiteToROOTColl_a Server WMI Class
The `SMS_SiteToROOTColl_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates an [SMS_Site Server WMI Class](../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object with an [SMS_Collection Server WMI Class](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object representing the root of the collections to which the site belongs.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteToROOTColl_a : SMS_BaseAssociation  
{  
      ref:SMS_Collection collection;  
      ref:SMS_Site site;  
};  
```  

## Methods  
 The `SMS_SiteToROOTColl_a` class does not define any methods.  

## Properties  
 `collection`  
 Data type: `ref:SMS_Collection`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Collection Server WMI Class](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object path for the root collection.  

 `site`  
 Data type: `ref:SMS_Site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Site Server WMI Class](../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object path for the site.  

## Remarks  
 Class qualifiers for this class include:  

-   Association: ToInstance  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
