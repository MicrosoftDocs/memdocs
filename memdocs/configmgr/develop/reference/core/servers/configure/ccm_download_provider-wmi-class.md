---
title: CCM_DownloadProvider Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the CCM_DownloadProvider class defines and registers a non-Microsoft download plug-in (alternate content) provider.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 888329e2-1af1-4233-8ea2-90a841356c38
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_DownloadProvider WMI Class
The **CCM_DownloadProvider** class, in Configuration Manager, defines and registers a non-Microsoft download plug-in (alternate content) provider.  

## Syntax  

```  
class CCM_DownloadProvider: CCM_Policy  
{  
    string  LogicalName;  
    string  CLSID;   
    uint32  Priority;   
    string  GlobalSettings; 
    string  PolicySource;
    string  Reserved;   
};  

```  

#### Parameters  
 `LogicalName`  
 Data type: String  

 Qualifiers: [in, RealKey, NotNull: ToInstance ToSubClass]  

 The name of the non-Microsoft provider. This field must match the value specified to the SMS provider.  

 `CLSID`  
 Data type: String  

 Qualifiers: [in, NotNull: ToInstance, ToSubClass]  

 The COM class ID corresponding to the interface implementation.  

 `Priority`  
 Data type: String  

 Qualifiers: [in, NotNull: ToInstance ToSubClass]  

 Priority in the face of multiple alternate provider choices. For future use. Must be nonzero.  

 `GlobalSettings`  
 Data type: String  

 Qualifiers: [in]  

 Provider specific data. Use this for any client-wide configuration for the provider.  

 `PolicySource`  
 Data type: String  

 Qualifiers: [in]  

 The source of the policy, typically "Local" when the instance is created on a client in the root\ccm\policy\machine\RequestedConfig namespace.  

 `Reserved`  
 Data type: String  

 Qualifiers: [in]  

 Reserved for future use.  

## Return Values  
 None.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
