---
title: AcceptEULA Method in SMS_SoftwareUpdate
titleSuffix: Configuration Manager
description: The AcceptEULA WMI class method accepts or declines the Microsoft Software License Terms of a configuration item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6edc5abf-0b72-43be-a5ee-5dda07fb90e8
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AcceptEULA Method in Class SMS_SoftwareUpdate
The `AcceptEULA` Windows Management Instrumentation (WMI) class method, in Configuration Manager, accepts or declines the Microsoft Software License Terms of a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AcceptEULA(  
     Boolean Accepted  
);  
```  

#### Parameters  
 `Accepted`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` if license terms are accepted.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application should call this method only if the `EulaExists` property is set to `true` in the configuration item for the software update. This property is defined in the [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)
