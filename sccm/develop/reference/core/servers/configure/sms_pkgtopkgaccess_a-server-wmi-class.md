---
title: "SMS_PkgToPkgAccess_a Class"
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
ms.assetid: 17a0dc88-ede7-43f5-9d36-f2fb38db0514searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_PkgToPkgAccess_a Server WMI Class
The `SMS_PkgToPkgAccess_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that uses the `PackageID` property to relate an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object with the [SMS_PackageAccessByUsers Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packageaccessbyusers-server-wmi-class.md) object used to access the package on its distribution points.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PkgToPkgAccess_a : SMS_BaseAssociation  
{  
      ref:SMS_Package package;  
      ref:SMS_PackageAccessByUsers pkgAccess;  
};  
```  

## Methods  
 The `SMS_PkgToPkgAccess_a` class does not define any methods.  

## Properties  
 `package`  
 Data type: `ref:SMS_Package`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object path.  

 `pkgAccess`  
 Data type: `ref:SMS_PackageAccessByUsers`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_PackageAccessByUsers Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packageaccessbyusers-server-wmi-class.md) object path.  

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
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [SMS_PackageAccessByUsers Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packageaccessbyusers-server-wmi-class.md)
