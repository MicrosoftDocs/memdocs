---
title: "GetChainedPullDPs Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 063a6390-8eb4-459d-b0b6-34592afe6326
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# GetChainedPullDPs Method in Class SMSDistributionPointInfo
The `GetChainedPullDPs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, ensures that when a source distribution point is assigned, a looping chain is not generated. (If distribution point 1 is the source of distribution point 2, and distribution point 2 is the source of distribution point 3, then distribution point 3 cannot be source of distribution point 1).  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetChainedPullDPs(  
     string SourceDPNALPath,  
     string ChainedDPs[]  
);  
```  

#### Parameters  
 `SourceDPNALPath`  
 Data type: `String`  

 Qualifiers: `[in]`  

 Source distribution point NAL path.  

 `ChainedDPs`  
 Data type: `String` Array  

 Qualifiers: `[out]`  

 An array of chained distribution points.  

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
