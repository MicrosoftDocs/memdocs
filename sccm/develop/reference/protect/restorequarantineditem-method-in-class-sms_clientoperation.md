---
title: "RestoreQuarantinedItem Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ad263099-312a-47bf-aaab-3debd3949c2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RestoreQuarantinedItem Method in Class SMS_ClientOperation
The `RestoreQuarantinedItem` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that restores quarantined items to all members in a collection infected by specified threat.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 RestoreQuarantinedItem   
{  
    [IN]    UInt64 ThreatID  
    [IN]    String ThreatName  
    [IN]    Boolean IncludeDependencies  
    [IN]    String TargetCollectionID  
    [OUT]   UInt32 OperationID  
};  
```  

## Parameters  
 `ThreatID`  
 Data type: `UInt64`  

 Qualifiers: [id("0"), in]  

 ThreatID.    

 `ThreatName`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 ThreatName.    

 `IncludeDependencies`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 IncludeDependencies.    

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("3"), in]  

 TargetCollectionID.    

 `OperationID`  
 Data type: `UInt32`  

 Qualifiers: [id("4"), out]  

 OperationID.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
