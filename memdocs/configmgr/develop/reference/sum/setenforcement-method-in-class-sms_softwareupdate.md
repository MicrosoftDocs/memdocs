---
title: SetEnforcement method in class SMS_SoftwareUpdate
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c4cfe110-e048-4393-92e3-cedc663fab0b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
description: Learn how to set policy enforcement rules for software updates by editing the 'SetEnforcement' class method in the Configuration Manager.
ms.reviewer: mstewart,aaroncz 
---
# SetEnforcement Method in Class SMS_SoftwareUpdate
The `SetEnforcement` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets policy enforcement for the software update.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetEnforcement(  
     Boolean Enforced,  
     DateTime EffectiveDate  
);  
```  

#### Parameters  
 `Enforced`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if policy enforcement is enabled for the configuration item.  

 `EffectiveDate`  
 Data type: `DateTime`  

 Qualifiers: [in]  

 The date and time, in Coordinated Universal Time (UTC), when the configuration item is compliant.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)
