---
description: Learn how to accept or decline the Microsoft Software License Terms of a configuration item using AcceptEULA class in Configuration Manager.
title: AcceptEULA Method in Class SMS_ConfigurationItem
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 28f37dfd-92bb-4ea7-8670-630b43d19a59
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AcceptEULA Method in Class SMS_ConfigurationItem
In Configuration Manager, the `AcceptEULA` Windows Management Instrumentation (WMI) class method accepts or declines the Microsoft Software License Terms of a configuration item.  

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

 `true` to accept the license terms.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application should call this method only if the `EulaExists` property is set to `true` in the configuration item. This property is defined in the [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)   
 [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md)
