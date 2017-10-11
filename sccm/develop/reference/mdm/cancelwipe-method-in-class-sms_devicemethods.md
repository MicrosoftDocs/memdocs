---
title: "CancelWipe Method"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 5cd73769-af3f-46c3-93d2-4b0391173b64searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CancelWipe Method in Class SMS_DeviceMethods
The `CancelWipe` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels a pending wipe request on mobile devices or Exchange ActiveSync devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CancelWipe(  
   UInt32 ResourceId  
);  
```  

#### Parameters  
 `ResourceId`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Identifier of the resource for which to cancel the wipe.  

## Return Values  
 An `SInt32`data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## See Also  
 [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)
