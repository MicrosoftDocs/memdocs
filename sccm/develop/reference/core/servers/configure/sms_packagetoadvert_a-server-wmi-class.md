---
title: "SMS_PackageToAdvert_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3ae13b60-46d9-44a5-90a7-cdb33f135e40
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PackageToAdvert_a Server WMI Class
The `SMS_PackageToAdvert_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object to the [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object that it advertises.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageToAdvert_a : SMS_BaseAssociation  
{  
      ref:SMS_Advertisement advert;  
      ref:SMS_Package package;  
};  
```  

## Methods  
 The `SMS_PackageToAdvert_a` class does not define any methods.  

## Properties  
 `advert`  
 Data type: `ref:SMS_Advertisement`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) object path.  

 `package`  
 Data type: `ref:SMS_Package`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object path.  

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
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
