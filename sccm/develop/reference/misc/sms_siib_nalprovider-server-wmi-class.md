---
title: "SMS_SIIB_NALProvider Class"
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
ms.assetid: 550a69c0-b9cc-4b65-b250-f1a2971bf615searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SIIB_NALProvider Server WMI Class
The `SMS_SIIB_NALProvider` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the network abstraction layer (NAL) provider configured for the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_NALProvider : SMS_SiteInstallItemBase   
{  
     UInt32 Flags;  
     String ItemName;  
     String ItemType;  
     String ProviderName;  
     String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_NALProvider` class does not define any methods.  

## Properties  
 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags indicating the use of the provider. Possible values are:  

 1  
 SERVER  

 2  
 ADMINUI  

 3  
 CLIENT  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ProviderName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the provider.  

 `Units`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
