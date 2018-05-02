---
title: "RemoveSource Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 683ee78e-5a8f-480c-8c95-db1333178c98
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RemoveSource Method in Class SMS_UserMachineRelationship
The `RemoveSource` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, removes a source for the relationship between a user and a device.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemoveSource(  
     uint32 SourceId  
);  
```  

#### Parameters  
 `SourceId`  
 Data type: `UInt32` Array  

 Qualifiers: `[in]`  

 Source object identifier for dependency.  

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
 [Application Model Server WMI Classes](../../../../../develop/reference/apps/application-management-server-wmi-classes.md)
