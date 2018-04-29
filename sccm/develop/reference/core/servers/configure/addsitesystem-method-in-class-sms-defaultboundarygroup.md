---
title: "AddSiteSystem Method"
titleSuffix: "Configuration Manager"
ms.date: "03/13/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 229fd29c-8651-4920-8482-194d52469e05
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# AddSiteSystem Method in Class SMS_DefaultBoundaryGroup
 The `AddSiteSystem` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds one or more site system servers to a default boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddSiteSystem(  
    String ServerNALPath[],
    UInt32 Flags[]   
);  
```  

### Parameters  
 `ServerNALPath`  
 Data type: `String` Array

 Qualifiers: [in]  

 Array of network abstraction layer (NAL) paths to one or more site system servers.  

 `Flags`  
 Data type: `UInt32` Array

 Qualifiers: [in]  

 Specifies the connection type of the boundary. Possible values are:  

|Value|Description|  
|---|---|  
|0|FAST|  
|1|SLOW|   

> [!NOTE]
> This parameter is no longer used for distribution points.

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
