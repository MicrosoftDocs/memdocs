---
title: "SMS_ProviderLocation Class"
titleSuffix: "Configuration Manager"
description: "The `SMS_ProviderLocation` Windows Management Instrumentation (WMI) class, in Configuration Manager, identifies the location of the SMS Provider for a site."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 18d57298-bdd6-437b-84b0-ead28c1d5d3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ProviderLocation Server WMI Class
The `SMS_ProviderLocation` Windows Management Instrumentation (WMI) class, in Configuration Manager, identifies the location of the SMS Provider for a site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ProviderLocation   
{  
     String Machine;  
     String NamespacePath;  
     Boolean ProviderForLocalSite;  
     String SiteCode;  
};  
```  

## Properties  
 `Machine`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the computer on which the SMS Provider resides.  

 `NamespacePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Full WMI path to the SMS Provider namespace.  

 `ProviderForLocalSite`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the SMS Provider is set as the local site server for the client.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Site code of the site.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 For information on using this class, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
