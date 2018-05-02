---
title: "GetFeatureState Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3350172b-3c4e-4cc5-af3e-cb94296ba052
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetFeatureState Method in Class SMS_Site
The `GetFeatureState` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the enabled/disabled state of a feature.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetFeatureState (  
     String SiteCode,  
     UInt32 FeatureID,  
     Boolean IsEnabled  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [in]  

 Site code of site to check. NULL indicates the current site.  

 `FeatureID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Feature identifier. Possible values are:  

|||  
|-|-|  
|1|SleepServer|  

 `IsEnabled`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the feature is enabled.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
