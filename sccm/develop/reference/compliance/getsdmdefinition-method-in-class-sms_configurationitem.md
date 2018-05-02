---
title: "GetSDMDefinition Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b2daf3d7-2073-48c5-be2d-1aef24c70f93
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetSDMDefinition Method in Class SMS_ConfigurationItem
The `GetSDMDefinition` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, retrieves the System Definition Model (SDM) definition of the configuration item in XML format.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSDMDefinition(  
     String SDMDefinition  
);  
```  

#### Parameters  
 `SDMDefinition`  
 Data type: `String`  

 Qualifiers: [out]  

 The SDM definition in XML format.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 For more information about SDM definitions, see About Authoring Configuration Baselines and Configuration Items.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)
