---
title: "GetEULA Method in SMS_SoftwareUpdate"
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
ms.assetid: bfab1311-5658-4992-9c56-a24b6cda73e5searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetEULA Method in Class SMS_SoftwareUpdate
The `GetEULA` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, gets the localized Microsoft Software License Terms content of a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetEULA(  
     String EULA  
);  
```  

#### Parameters  
 `EULA`  
 Data type: `String`  

 Qualifiers: [out]  

 The Microsoft Software License Terms.  

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
