---
title: "SetNextID Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6df3e624-10d6-42e0-b98d-86352df0751e
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# SetNextID Method in Class SMS_Advertisement
The `SetNextID` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the ID number that will be used for the next advertisement created.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetNextID (  
    UInt32 NextID  
);  

```  

#### Parameters  
 `NextID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID number for the next advertisement.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
