---
description: Learn how to run a synchronous discovery operation for the provided synclet using IAppManagementHandler::DiscoveryApp.
title: "IAppManagementHandler::DiscoverApp"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 818e9387-2599-405e-913a-642e96c97fd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# IAppManagementHandler::DiscoverApp Method
The `IAppManagementHandler::DiscoverApp` method, in Configuration Manager, runs a synchronous discovery operation for the provided synclet.  

## Syntax  

```  
[IDL]  
HRESULT DiscoverApp(  
     HANDLE hUserToken,  
     LPCWSTR szDeploymentTypeId,  
     DWORD dwDeploymentTypeRevision,  
     AppDeploymentTypeData* pDetectResult  
);  
```  

#### Parameters  
 `hUserToken`  
 Data type: `HANDLE`  

 Qualifiers: [in]  

 The user token. If it is null, the action is for computer. If it is not NULL, the action is for the user.  

 `szDeploymentTypeId`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 .   

 `dwDeploymentTypeRevision`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 .   

 `pDetectResult`  
 Data type: `AppDeploymentTypeData`  

 Qualifiers: [out]  

 .   

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully.  All other return values indicate failure.  

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
