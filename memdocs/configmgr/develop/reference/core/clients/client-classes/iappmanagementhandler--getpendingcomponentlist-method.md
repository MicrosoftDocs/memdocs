---
title: "IAppManagementHandler::GetPendingComponentList"
titleSuffix: Configuration Manager
description: "The IAppManagementHandler::GetPendingComponentList method gets the pending component list for a specified deployment type."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: d769f0da-1b46-4a3b-9dc7-f14d7a489020
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IAppManagementHandler::GetPendingComponentList Method
The `IAppManagementHandler::GetPendingComponentList` method, in Configuration Manager, gets the pending component list for a specified deployment type. This is an optional method for the application deployment type handler. It's called if the handler returns a status of "PendingUpdate" for the `EnforceApp` method.  Software Center presents a list of these components to the end user, which need to be closed in order for the `EnforceApp` method to succeed.  

## Syntax  

```  
[IDL]  
HRESULT GetPendingComponentList(  
     IWbemClassObject* pDeliveryTypeSynclet,  
     LPWSTR* pwszPendingComponentList  
);  
```  

#### Parameters  
 `pDeliveryTypeSynclet`  
 Data type: `IWbemClassObject`  

 Qualifiers: [in]  

 The WMI object for the installation synclet which is associated with the application deployment type that is being installed.  

 `pwszPendingComponentList`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 The pending component list in XML format.  

## Return Values  
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

 E_NOTIMPL  
 The method isn't supported by the handler.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
