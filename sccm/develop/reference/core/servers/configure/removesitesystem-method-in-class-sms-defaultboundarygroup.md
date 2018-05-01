---
title: "RemoveSiteSystem Method"
titleSuffix: "Configuration Manager"
ms.date: "03/13/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4cccccef-404a-4d15-adef-6cfc77502df5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RemoveSiteSystem Method in Class SMS_DefaultBoundaryGroup
 The `RemoveSiteSystem` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes one or more site system servers from a default boundary group.    

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RemoveSiteSystem(  
    String ServerNALPath[]  
);  
```  

### Parameters  
 `ServerNALPath`  
 Data type: `String`  

 Qualifiers: [in]  

 Array of network abstraction layer (NAL) paths to one or more site system servers within the boundary group.

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DefaultBoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms-defaultboundarygroup-server-wmi-class.md)
