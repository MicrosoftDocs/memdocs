---
title: "SMS_CollectionToPkgAdvert_a Class"
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
ms.assetid: 4ca32d14-75da-4af6-aa74-9c5720a2a56esearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CollectionToPkgAdvert_a Server WMI Class
The `SMS_CollectionToPkgAdvert_a` association Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that uses the `CollectionID` property to relate an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object with its target [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionToPkgAdvert_a : SMS_BaseAssociation  
{  
      ref:SMS_Advertisement advert;  
      ref:SMS_Collection collection;  
};  
```  

## Methods  
 The `SMS_CollectionToPkgAdvert_a` class does not define any methods.  

## Properties  
 `advert`  
 Data type: `ref:SMS_Advertisement`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object path.  

 `collection`  
 Data type: `ref:SMS_Collection`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object path.  

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
 [Collections Server WMI Classes](../../../../../develop/reference/core/clients/collections/collections-server-wmi-classes.md)
