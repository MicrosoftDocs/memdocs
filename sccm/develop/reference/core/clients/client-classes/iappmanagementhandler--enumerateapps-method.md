---
title: "IAppManagementHandler::EnumerateApps"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0e4b2ecd-ebc1-4a38-af80-e3d198d6a1a7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# IAppManagementHandler::EnumerateApps Method
The `IAppManagementHandler::EnumerateApps` method, in Configuration Manager, runs a synchronous discovery operation for the provided synclet.  

## Syntax  

```  
[IDL]  
HRESULT EnumerateApps(  
     HANDLE hUserToken,  
     AppDeploymentTypeData* pDetectResult  
);  
```  

#### Parameters  
 `hUserToken`  
 Data type: `HANDLE`  

 Qualifiers: [in]  

 The user token. If it is null, the action is for computer. If it is not NULL, the action is for the user.  

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
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
