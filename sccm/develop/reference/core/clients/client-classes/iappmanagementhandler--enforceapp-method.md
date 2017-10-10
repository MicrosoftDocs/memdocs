---
title: "IAppManagementHandler::EnforceApp"
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
ms.assetid: 3c554beb-fe34-42ec-bc02-d427238ec811searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IAppManagementHandler::EnforceApp Method
The `IAppManagementHandler::EnforceApp` method, in Configuration Manager, starts the installation of a specific application.  

 If the handler supports reconnection, it must return a valid reconnect instance to `ppReconnectData`. If for whatever reason the installation cannot start, but is not in an error state, for example, no user token to display, then the handler should return `S_FALSE`.  

## Syntax  

```  
[IDL]  
HRESULT EnforceApp(  
     AppAction eEnforceAction,  
     HANDLE hUserToken,  
     DWORD dwSessionId,  
     IWbemClassObject* pHandlerSynclet,  
     LPCWSTR szLocalContentPath,  
     HANDLE* phInstallProcess,  
     DWORD* pdwExitCode,  
     LPWSTR* ppszExecutionStatus,  
     IWbemClassObject** ppReconnectData  
);  
```  

#### Parameters  
 `eEnforceAction`  
 Data type: `AppAction`  

 Qualifiers: [in]  

 .   

 `hUserToken`  
 Data type: `HANDLE`  

 Qualifiers: [in]  

 .   

 `dwSessionId`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 .   

 `pHandlerSynclet`  
 Data type: `IWbemClassObject`  

 Qualifiers: [in]  

 .   

 `szLocalContentPath`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 .   

 `phInstallProcess`  
 Data type: `HANDLE`  

 Qualifiers: [out]  

 .   

 `pdwExitCode`  
 Data type: `DWORD`  

 Qualifiers: [out]  

 .   

 `ppszExecutionStatus`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 .   

 `ppReconnectData`  
 Data type: `IWbemClassObject`  

 Qualifiers: [out]  

 .   

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure. If for whatever reason the installation cannot start, but is not in an error state, for example, no user token to display UI, then the handler should return `S_FALSE`  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [IAppManagementHandler Interface](../../../../../develop/reference/core/clients/client-classes/iappmanagementhandler-interface.md)   
 [Application Management Client Interfaces](../../../../../develop/reference/core/clients/client-classes/application-management-client-interfaces.md)   
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
