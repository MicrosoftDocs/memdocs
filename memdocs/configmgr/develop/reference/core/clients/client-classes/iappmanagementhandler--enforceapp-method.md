---
title: "IAppManagementHandler::EnforceApp"
titleSuffix: "Configuration Manager"
description: "A method that starts the installation of a specific application."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3c554beb-fe34-42ec-bc02-d427238ec811
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
