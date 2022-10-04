---
description: Learn how to relate an SMS Advertisement Server class object with the SMS Site Server class object that created the advertisement.
title: SMS_AdvertToSourceSite_a Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9e9f3288-1531-4f95-85a5-33971ef3e8e1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_AdvertToSourceSite_a Server WMI Class
The `SMS_AdvertToSourceSite_a` association Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object with the [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object that created the advertisement.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdvertToSourceSite_a : SMS_BaseAssociation  
{  
   ref:SMS_Site advertSourceSite;  
      ref:SMS_Advertisement ownedAdvert;  
};  
```  

## Methods  
 The `SMS_AdvertToSourceSite_a` class does not define any methods.  

## Properties  
 `advertSourceSite`  
 Data type: `ref:MS_Site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object path.  

 `ownedAdvert`  
 Data type: `ref:SMS_Advertisement`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object path.  

## Remarks  
 Class qualifiers for this class include:  

- Association: ToInstance  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)   
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)
