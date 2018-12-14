---
title: "SMS_PackageToSourceSite_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 44bfdfde-3c1f-4a86-b4e9-1ec81cfede1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PackageToSourceSite_a Server WMI Class
The `SMS_PackageToSourceSite_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that uses the `SiteCode` property to relate an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object to the [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object for the site that created the package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageToSourceSite_a : SMS_BaseAssociation  
{  
      ref:SMS_Package ownedPackage;  
      ref:SMS_Site pkgSourcesite;  
};  
```  

## Methods  
 The `SMS_PackageToSourceSite_a` class does not define any methods.  

## Properties  
 `ownedPackage`  
 Data type: `ref:SMS_Package`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object path.  

 `pkgSourcesite`  
 Data type: `ref:SMS_Site`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object path.  

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
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
