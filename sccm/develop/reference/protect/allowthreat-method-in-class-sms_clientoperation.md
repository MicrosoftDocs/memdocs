---
title: "AllowThreat Method"
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
ms.assetid: 601d8cac-f0a7-4d98-82b6-60d3a8080b23searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# AllowThreat Method in Class SMS_ClientOperation
The `AllowThreat` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that allows the specified threat (identified by `ThreatID`) to all members in a specific collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 AllowThreat   
{  
    [IN]    UInt64 ThreatID  
    [IN]    String AllowSettingsUniqueID  
    [IN]    String TargetCollectionID  
    [OUT]   UInt32 OperationID  
};  
```  

## Parameters  
 `ThreatID`  
 Data type: `UInt64`  

 Qualifiers: [id("0"), in]  

 Threat identifier.  

 `AllowSettingsUniqueID`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Antimalware settings (with allow threat identifier enabled) unique identifier.  

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 Identifier of target collection.  

 `OperationID`  
 Data type: `UInt32`  

 Qualifiers: [id("3"), out]  

 Unique identifier for the operation.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ClientOperation Server WMI Class](../../../develop/reference/protect/sms_clientoperation-server-wmi-class.md)
