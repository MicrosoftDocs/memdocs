---
title: "IAppManagementHandler::CheckReconnectData"
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
ms.assetid: ca2e0cca-4858-437e-bfb1-45e97f3733f7searchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IAppManagementHandler::CheckReconnectData Method
The `IAppManagementHandler::CheckReconnectData` method, in Configuration Manager, checks whether the reconnection data is valid.  

## Syntax  

```  
[IDL]  
HRESULT CheckReconnectData(  
     IWbemClassObject* pReconnectData,  
     BOOL* pfIsValid,  
     BOOL* pfEnforcementFinished  
);  
```  

#### Parameters  
 `pReconnectData`  
 Data type: `IWbemClassObject`  

 Qualifiers: [in]  

 .   

 `pfIsValid`  
 Data type: `BOOL`  

 Qualifiers: [out]  

 .   

 `pfEnforcementFinished`  
 Data type: `BOOL`  

 Qualifiers: [out]  

 .   

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
