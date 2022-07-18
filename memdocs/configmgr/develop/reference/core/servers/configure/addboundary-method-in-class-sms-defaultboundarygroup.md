---
description: Learn how to add one or more boundaries to a default boundary group using AddBoundary in Configuration Manager.
title: AddBoundary method in class SMS_DefaultBoundaryGroup
titleSuffix: "Configuration Manager"
ms.date: "03/13/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: aae63f60-858e-4467-9c70-f6d94ce53d57
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AddBoundary Method in Class SMS_DefaultBoundaryGroup
 The `AddBoundary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds one or more boundaries to a default boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddBoundary(  
    UInt32 BoundaryID[]   
);  
```  

### Parameters  
 `BoundaryID`  
 Data type: `UInt32` Array

 Qualifiers: [in]  

 Array of boundary IDs.  

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
