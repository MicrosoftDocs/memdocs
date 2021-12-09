---
title: "AddDistributionPoints Method in Class SMS_ContentPackage"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c9246eea-5960-4ed8-a042-6e3ce5689eca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AddDistributionPoints Method in Class SMS_ContentPackage
The `AddDistributionPoints` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds the distribution points to the [SMS_ContentPackage Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_contentpackage-server-wmi-class.md) content package.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
sint32 AddDistributionPoints (  
     string SiteCode[],  
     string NALPath[]  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 The code for the site to which to add distribution points.  

 `NALPath`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 Network abstraction layer (NAL) path to the distribution points.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
