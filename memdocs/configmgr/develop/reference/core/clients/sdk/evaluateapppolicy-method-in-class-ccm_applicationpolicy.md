---
title: "EvaluateAppPolicy Method"
description: Learn how the EvaluateAppPolicy Windows Management Instrumentation (WMI) class method, in Configuration Manager, that evaluates application policy.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 96b4dfce-3e5f-4e88-a19c-2429b2b1aae4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# EvaluateAppPolicy Method in Class CCM_ApplicationPolicy
The `EvaluateAppPolicy` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that evaluates application policy.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 EvaluateAppPolicy   
{  
    [IN]    String PolicyId  
    [IN]    String PolicyRevision  
    [IN]    Boolean IsMachineTarget  
    [IN]    String Priority  
    [IN]    Boolean IsEnforceAction  
    [IN]    String MTCToken  
    [IN]    String SDKCallerId  
    [OUT]   String JobId  
};  
```  

## Parameters  
 `PolicyId`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Policy identifier.    

 `PolicyRevision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Policy revision.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `True` if this is a device targeted application.      

 `Priority`  
 Data type: `String`  

 Qualifiers: [id("3"), in, valuemap]  

 Priority. Possible values are:   

|Value|
|-|  
|Foreground|  
|High|  
|Normal|  
|Low|  

 `IsEnforceAction`  
 Data type: `Boolean`  

 Qualifiers: [id("4"), in]  

 `True` if the action will be enforced.    

 `MTCToken`  
 Data type: `String`  

 Qualifiers: [id("5"), in]  

 MTC token.    

 `SDKCallerId`  
 Data type: `String`  

 Qualifiers: [id("6"), in]  

 SDK caller identifier.    

 `JobId`  
 Data type: `String`  

 Qualifiers: [id("7"), out]  

 Job identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
