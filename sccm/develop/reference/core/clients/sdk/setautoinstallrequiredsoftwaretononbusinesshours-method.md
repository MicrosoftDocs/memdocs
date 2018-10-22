---
title: "SetAutoInstallRequiredSoftwaretoNonBusinessHours Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b02219c8-09b1-4328-8b5c-796d93bc62c0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SetAutoInstallRequiredSoftwaretoNonBusinessHours Method in Class CCM_ClientUXSettings
The `SetAutoInstallRequiredSoftwaretoNonBusinessHours` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that sets the value for `AutomaticallyInstallSoftware`.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 SetAutoInstallRequiredSoftwaretoNonBusinessHours   
{  
    [IN]    Boolean AutomaticallyInstallSoftware  
};  
```  

## Parameters  
 `AutomaticallyInstallSoftware`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), in]  

 `true` if required software should be automatically installed during non-business hours.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
