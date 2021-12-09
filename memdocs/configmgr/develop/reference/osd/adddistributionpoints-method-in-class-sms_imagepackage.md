---
title: "AddDistributionPoints Method in SMS_ImagePackage"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0beeb890-054c-488c-8fa2-e5c1302a7d72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AddDistributionPoints Method in Class SMS_ImagePackage
The `AddDistributionPoints` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds the list of distribution points for the image package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddDistributionPoints(  
      String SiteCode[],  
      String NALPath[]  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The code for the site to which to add the distribution points.  

 `NALPath`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Network abstraction layer (NAL) path to the distribution points.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 It is not necessary to refresh the distribution points when using this method.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ImagePackage Server WMI Class](../../../develop/reference/osd/sms_imagepackage-server-wmi-class.md)
